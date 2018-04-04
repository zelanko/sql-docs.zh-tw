---
title: "應用程式層級資料分割 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 162d1392-39d2-4436-a4d9-ee5c47864c5a
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15f07a9dd757fe2cb392a42ab7ab726ccac1f8d1
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2018
---
# <a name="application-level-partitioning"></a>應用程式層級資料分割
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此應用程式會處理訂單。 未在最近的訂單上進行多項處理。 舊訂單上未進行多項處理。 最近的訂單位於記憶體最佳化的資料表中。 舊訂單位於磁碟資料表中。 *hotDate* 之後的所有訂單都位於記憶體最佳化資料表中。 *hotDate* 之前的所有訂單都位於磁碟資料表中。 假設有一個具有許多並行交易的極端 OLTP 工作負載。 即使有數項並行交易嘗試變更 *hotDate*，仍必須強制執行此商務規則 (記憶體最佳化資料表中最近的訂單)。  
  
 此範例不會針對磁碟資料表使用分割區資料表，但會使用第三個資料表來追蹤兩個資料表之間的明確分割點。 分割點可用來確定新插入的資料一律會根據日期插入適當的資料表。 其也可用來判斷資料的位置。 晚抵達的資料仍會插入適當的資料表。  
  
 如需相關範例，請參閱 [分割記憶體最佳化資料表的應用程式模式](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)。  
  
## <a name="code-listing"></a>程式碼清單  
  
```sql  
USE MASTER  
GO  
IF NOT EXISTS(SELECT name FROM sys.databases WHERE name = 'hkTest')  
  
CREATE DATABASE hkTest  
-- enable for In-Memory OLTP - change file path as needed  
ALTER DATABASE hkTest ADD FILEGROUP hkTest_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hkTest ADD FILE( NAME = 'hkTest_mod' , FILENAME = 'c:\data\hkTest_mod') TO FILEGROUP hkTest_mod;  
GO  
  
use hkTest  
go  
  
-- create memory-optimized table   
if OBJECT_ID(N'hot',N'U') IS NOT NULL  
   drop table [hot]  
  
create table hot   
   (id int not null primary key nonclustered,  
   orderDate datetime not null,  
   custName nvarchar(10) not null  
) with (memory_optimized=on)  
go  
  
-- create disk-based table for older order data  
if OBJECT_ID(N'cold',N'U') IS NOT NULL  
   drop table [cold]  
  
create table cold (  
   id int not null primary key,   
   orderDate datetime not null,   
   custName nvarchar(10) not null  
)  
go  
  
-- the hotDate is maintained in this memory-optimized table. The current hotDate is always the single date in this table  
if OBJECT_ID(N'hotDataSplit') IS NOT NULL  
   drop table [hotDataSplit]  
  
create table hotDataSplit (  
   hotDate datetime not null primary key nonclustered hash with (bucket_count = 1)  
) with (memory_optimized=on)  
go  
  
--  Stored Procedures  
--  set the hotDate  
--  snapshot: if any other transaction tries to update the hotDate, it will fail immediately due to a  
--  write/write conflict  
if OBJECT_ID(N'usp_hkSetHotDate') IS NOT NULL  
   drop procedure usp_hkSetHotDate  
go  
  
create procedure usp_hkSetHotDate @newDate datetime  
   with native_compilation, schemabinding, execute as owner  
   as begin atomic with  
   (  
      transaction isolation level = snapshot,  
      language = N'english'  
   )  
  
   delete from dbo.hotDataSplit  
   insert dbo.hotDataSplit values (@newDate)  
   end  
go  
  
-- extract data up to a certain date [presumably the new hotDate]  
-- must be serializable, because you don't want to delete rows that are not returned  
if OBJECT_ID(N'usp_hkExtractHotData') IS NOT NULL  
   drop procedure usp_hkExtractHotData  
go  
create procedure usp_hkExtractHotData @hotDate datetime  
   with native_compilation, schemabinding, execute as owner  
   as begin atomic with  
   (  
      transaction isolation level = serializable,  
      language = N'english'  
)  
   select id, orderDate, custName from dbo.hot where orderDate < @hotDate  
   delete from dbo.hot where orderDate < @hotDate  
end  
go  
  
-- insert order  
-- inserts an order either in recent or older table, depending on the current hotDate  
-- it is important that the SP for retrieving the hotDate is repeatableread, in order to ensure that  
-- the hotDate is not changed before the decision is made where to insert the order  
-- note that insert operations [in both disk-based and memory-optimized tables] are always fully isolated, so the transaction  
-- isolation level has no impact on the insert operations; this whole transaction is effectively repeatableread  
if OBJECT_ID(N'usp_InsertOrder') IS NOT NULL  
   drop procedure usp_InsertOrder  
go  
  
create procedure usp_InsertOrder(@id int, @orderDate date, @custName nvarchar(10))  
   as begin  
   SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
   begin tran  
      -- get hot date under repeatableread isolation; this is to guarantee it does not change before the insert is executed  
      declare @hotDate datetime  
      set @hotDate = (select hotDate from hotDataSplit with (repeatableread))  
  
      if (@orderDate >= @hotDate) begin  
         insert into hot values (@id, @orderDate, @custName)  
      end  
      else begin  
         insert into cold values (@id, @orderDate, @custName)  
      end  
   commit tran  
end  
go  
  
-- change hot date  
-- changes the hotDate and moves the rows between the recent and older order tables as appropriate  
-- the hotDate is updated in this transaction; this means that if the hotDate is changed by another transaction  
--   the update will fail due to a write/write conflict and the transaction is rolled back  
--   therefore, the initial (snapshot) access of the hotDate is effectively repeatable read  
if OBJECT_ID(N'usp_ChangeHotDate') IS NOT NULL  
   drop procedure usp_ChangeHotDate  
go  
create procedure usp_ChangeHotDate(@newHotDate datetime)  
as  
begin  
   SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
   begin tran  
       declare @oldHotDate datetime  
      set @oldHotDate = (select hotDate from hotDataSplit with (snapshot))  
  
       -- get hot date under repeatableread isolation; this is to guarantee it does not change before the insert is executed  
      if (@oldHotDate < @newHotDate) begin  
         insert into cold exec usp_hkExtractHotData @newHotDate  
      end  
      else begin  
         insert into hot select * from cold with (serializable) where orderDate >= @newHotDate  
         delete from cold with (serializable) where orderDate >= @newHotDate  
      end  
      exec usp_hkSetHotDate @newHotDate  
   commit tran  
end  
go  
  
--  Deploy and populate tables  
-- cleanup  
delete from cold  
go  
  
-- init hotDataSplit  
exec usp_hkSetHotDate '2012-1-1'   
go  
  
-- verify hotDate  
select * from hotDataSplit  
go  
  
EXEC usp_InsertOrder 1, '2011-11-14', 'cust1'  
EXEC usp_InsertOrder 2, '2012-3-4', 'cust1'  
EXEC usp_InsertOrder 3, '2011-1-23', 'cust1'  
EXEC usp_InsertOrder 4, '2011-8-6', 'cust1'  
EXEC usp_InsertOrder 5, '2010-11-1', 'cust1'  
EXEC usp_InsertOrder 6, '2012-1-9', 'cust1'  
EXEC usp_InsertOrder 7, '2012-2-14', 'cust1'  
EXEC usp_InsertOrder 8, '2010-1-17', 'cust1'  
EXEC usp_InsertOrder 9, '2012-3-8', 'cust1'  
EXEC usp_InsertOrder 10, '2011-9-24', 'cust1'  
go  
  
--  Demo Portion  
-- verify contents of the tables  
-- hotDate is 2012-1-1  
-- all orders from 2012 are in the recent table  
-- all orders before 2012 are in the older order table  
  
-- query hot data  
select * from hot order by orderDate desc  
  
-- query cold date  
select * from cold order by orderDate desc  
  
-- move hot date to Mar 2012  
EXEC usp_ChangeHotDate '2012-03-01'  
  
-- Verify that all orders before Mar 2012 were moved to older order table  
-- query hot data  
select * from hot order by orderDate desc  
  
-- query old data  
select * from cold order by orderDate desc  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 程式碼範例](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)  
  
  
