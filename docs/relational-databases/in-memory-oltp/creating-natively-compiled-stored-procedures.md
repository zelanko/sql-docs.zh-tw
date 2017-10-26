---
title: "建立原生編譯的預存程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f0ebadeaa959c6eb148cdd9a9d6e0a1019d858ab
ms.openlocfilehash: 413be658a429308744b303d2d3ef82892c964c5a
ms.contentlocale: zh-tw
ms.lasthandoff: 07/27/2017

---
# <a name="creating-natively-compiled-stored-procedures"></a>建立原生編譯的預存程序
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  原生編譯預存程序不會實作完整 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可程式性和查詢介面區。 某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建構無法在原生編譯的預存程序內使用。 如需詳細資訊，請參閱 [原生編譯的 T-SQL 模組支援的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)。  
  
 但有幾個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能只可供原生編譯的預存程序使用：  
  
-   不可部分完成的區塊。 如需詳細資訊，請參閱 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  
  
-   參數和變數上的 **NOT NULL** 限制式。 您不能指派 **NULL** 值給宣告為 **NOT NULL**的參數或變數。 如需詳細資訊，請參閱 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)。  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"**; -- *(必須初始化為值。)*  
  
    -   SET @myVarchar **= null**; -- *(編譯，但是在執行階段期間會失敗。)*  
  
-   原生編譯預存程序的結構描述繫結。  
  
 使用 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)建立原生編譯的預存程序。 下列範例會顯示記憶體最佳化的資料表以及用來將資料列插入資料表中的原生編譯預存程序。  
  
```tsql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 在程式碼範例中， **NATIVE_COMPILATION** 表示這個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序是原生編譯的預存程序。 以下是必要的選項：  
  
|選項|描述|  
|------------|-----------------|  
|**SCHEMABINDING**|原生編譯的預存程序必須繫結至其所參考之物件的結構描述。 這表示，此程序所參考的資料表將無法卸除。 此程序中參考的資料表必須包含其結構描述名稱，而且查詢中不允許使用萬用字元 (\*) (表示沒有 `SELECT * from...`)。 只有這個**版本中的原生編譯預存程序才支援** SCHEMABINDING [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**BEGIN ATOMIC**|原生編譯的預存程序主體必須剛好由一個不可部分完成的區塊所組成。 不可部分完成的區塊保證會以不可部分完成的方式執行預存程序。 如果此程序在使用中交易的內容之外叫用，它將會開始新的交易，該交易會在不可部分完成的區塊結尾認可。 原生編譯預存程序中不可部分完成的區塊有兩個必要選項：<br /><br /> **TRANSACTION ISOLATION LEVEL** 如需支援的隔離等級，請參閱 [記憶體最佳化資料表的交易隔離等級](http://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) 。<br /><br /> **LANGUAGE**。 預存程序的語言必須設定為其中一個可用語言或語言別名。|  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  

