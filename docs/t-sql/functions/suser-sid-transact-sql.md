---
title: SUSER_SID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a31be66b07c6d5c463f5220e6359942cd507849b
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981739"
---
# <a name="suser_sid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回指定登入名稱的安全性識別碼 (SID)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>引數  
 **'** *login* **'**  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本
  
 這是使用者的登入名稱。 *login* 為 **sysname**。 選擇性的 *login* 可為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者或群組。 若沒有指定 *login*，則會傳回目前安全性內容的相關資訊。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
 *Param2*  
**適用於**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本
  
 指定是否要驗證登入名稱。 *Param2* 的類型為 **int** 且為選擇性。 當 *Param2* 為 0 時，不會驗證登入名稱。 當 *Param2* 未指定為 0 時，會驗證 Window 登入名稱與儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的登入名稱完全相同。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary(85)**  
  
## <a name="remarks"></a>Remarks  
 SUSER_SID 可在 ALTER TABLE 或 CREATE TABLE 中，用來當做 DEFAULT 條件約束使用。 SUSER_SID 可用在選取清單、WHERE 子句及任何允許使用運算式的位置中。 SUSER_SID 後面一律必須接著括號，即使未指定任何參數，也是如此。  
  
 當呼叫 SUSER_SID 時，如果未設定引數，它會傳回目前安全性內容的 SID。 當利用 EXECUTE AS，在已切換內容的批次內，未設定引數的情況下呼叫 SUSER_SID 時，它會傳回模擬內容的 SID。 當從模擬內容呼叫時，SUSER_SID(ORIGINAL_LOGIN()) 會傳回原始內容的 SID。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序與 Windows 定序不同時，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 以不同的格式儲存登入，SUSER_SID 可能會失敗。 例如，如果 Windows 電腦 TestComputer 具有登入使用者，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將該登入儲存為 TESTCOMPUTER\User，則查閱 TestComputer\User 登入時可能無法正確地解析登入名稱。 若要略過登入名稱的驗證作業，請使用 *Param2*。 不同的定序通常是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤 15401 的原因：  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-suser_sid"></a>A. 使用 SUSER_SID  
 下列範例會傳回目前安全性內容的安全性識別碼 (SID)。  
  
```  
SELECT SUSER_SID();  
```  
  
### <a name="b-using-suser_sid-with-a-specific-login"></a>B. 搭配特定登入使用 SUSER_SID  
 下列範例會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa` 登入的安全性識別碼。  
  
**適用於**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-suser_sid-with-a-windows-user-name"></a>C. 搭配使用 SUSER_SID 與 Windows 使用者名稱  
 下列範例會傳回 Windows 使用者 `London\Workstation1` 的安全性識別碼。  
  
**適用於**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-suser_sid-as-a-default-constraint"></a>D. 使用 SUSER_SID 做為 DEFAULT 條件約束  
 下列範例會利用 `SUSER_SID` 來做為 `DEFAULT` 陳述式中的 `CREATE TABLE` 條件約束。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. 比較 Windows 登入名稱與 SQL Server 中所儲存的登入名稱  
 下列範例示範如何使用 *Param2* 從 Windows 取得 SID，並使用該 SID 作為 `SUSER_SNAME` 函式的輸入。 此範例以 Windows 中的儲存格式 (`TestComputer\User`) 提供登入，並以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的儲存格式 (`TESTCOMPUTER\User`) 傳回登入。  
  
**適用於**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>另請參閱  
 [ORIGINAL_LOGIN &#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary 和 varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
