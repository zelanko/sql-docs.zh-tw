---
title: "SYSTEM_USER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSTEM_USER_TSQL
- SYSTEM_USER
dev_langs:
- TSQL
helpviewer_keywords:
- current user names
- system-supplied user names [SQL Server]
- users [SQL Server], logins
- logins [SQL Server], identification name
- current system user names
- SYSTEM_USER function
- inserting system user name into table
- system usernames [SQL Server]
- users [SQL Server], names
ms.assetid: 565984cd-60c6-4df7-83ea-2349b838ccb2
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3f13d5db5d7787a60c455edc64644f4c23779fc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="systemuser-transact-sql"></a>SYSTEM_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  如果未指定預設值，則可將系統提供的目前登入值插入資料表中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SYSTEM_USER  
```  
  
## <a name="return-types"></a>傳回類型  
 **nchar**  
  
## <a name="remarks"></a>備註  
 您可以在 CREATE TABLE 和 ALTER TABLE 陳述式中，搭配 DEFAULT 條件約束使用 SYSTEM_USER 函數。 您也可以把它當作任何標準函數使用。  
  
 如果使用者名稱和登入名稱不同，SYSTEM_USER 便會傳回登入名稱。  
  
 如果目前的使用者登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 Windows 驗證，system_user 便會傳回 Windows 登入識別名稱格式：*網域*\\*user_login_name*. 不過，如果目前使用者是利用 SQL Server 驗證登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SYSTEM_USER 便會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入識別名稱，例如，以 `WillisJo` 登入的使用者，就傳回 `WillisJo`。  
  
 SYSTEM_USER 會傳回目前執行內容的名稱。 如果 EXECUTE AS 陳述式已用來切換內容，SYSTEM_USER 便會傳回模擬內容的名稱。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-systemuser-to-return-the-current-system-user-name"></a>A. 利用 SYSTEM_USER 傳回目前系統使用者名稱  
 下列範例會宣告一個 `char` 變數，將 `SYSTEM_USER` 的目前值儲存在變數中，然後再列印儲存在變數中的值。  
  
```  
DECLARE @sys_usr char(30);  
SET @sys_usr = SYSTEM_USER;  
SELECT 'The current system user is: '+ @sys_usr;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `----------------------------------------------------------`  
  
 `The current system user is: WillisJo`  
  
 `(1 row(s) affected)`  
  
### <a name="b-using-systemuser-with-default-constraints"></a>B. 使用 SYSTEM_USER 搭配 DEFAULT 條件約束  
 下列範例會建立一份資料表，將 `SYSTEM_USER` 做為 `DEFAULT` 資料行的 `SRep_tracking_user` 條件約束。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.Sales_Tracking  
(  
    Territory_id int IDENTITY(2000, 1) NOT NULL,  
    Rep_id  int NOT NULL,  
    Last_sale datetime NOT NULL DEFAULT GETDATE(),  
    SRep_tracking_user varchar(30) NOT NULL DEFAULT SYSTEM_USER  
);  
GO  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (151);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (293, '19980515');  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (27882, '19980620');  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (21392);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (24283, '19981130');  
GO  
```  
  
 下列查詢會選取 `Sales_Tracking` 資料表中的所有資訊：  
  
```  
SELECT * FROM Sales_Tracking ORDER BY Rep_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Territory_id Rep_id Last_sale            SRep_tracking_user`  
  
 `-----------  ------ -------------------- ------------------`  
  
 `2000         151    Mar 4 1998 10:36AM   ArvinDak`  
  
 `2001         293    May 15 1998 12:00AM  ArvinDak`  
  
 `2003         21392  Mar 4 1998 10:36AM   ArvinDak`  
  
 `2004         24283  Nov 3 1998 12:00AM   ArvinDak`  
  
 `2002         27882  Jun 20 1998 12:00AM  ArvinDak`  
  
 `(5 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-systemuser-to-return-the-current-system-user-name"></a>C： 利用 SYSTEM_USER 傳回目前的系統使用者名稱  
 下列範例會傳回目前的值`SYSTEM_USER`。  
  
```  
SELECT SYSTEM_USER;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;TRANSACT-SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [使用者 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/user-transact-sql.md)  
  
  


