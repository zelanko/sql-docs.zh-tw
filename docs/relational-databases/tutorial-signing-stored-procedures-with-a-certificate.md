---
title: 教學課程：使用憑證簽署預存程序 | Microsoft 文件
ms.custom: ''
ms.date: 08/23/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.topic: quickstart
applies_to:
- SQL Server 2016
helpviewer_keywords:
- signing stored procedures tutorial [SQL Server]
ms.assetid: a4b0f23b-bdc8-425f-b0b9-e0621894f47e
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2adac6728e7c288a50d525a0760a98a26c5b2b2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021082"
---
# <a name="tutorial-signing-stored-procedures-with-a-certificate"></a>教學課程：使用憑證簽署預存程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
這個教學課程說明如何使用由 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]產生的憑證來簽署預存程序。  
  
> [!NOTE]  
> 若要執行本教學課程中的程式碼，您必須設定使用混合模式安全性，並已安裝 AdventureWorks2017 資料庫。   
  
當您希望對預存程序加諸必要的權限，卻又不想明確將這些權限授與使用者時，使用憑證簽署預存程序就非常有用。 儘管透過其他方式也能達到這個目的 (比方使用 EXECUTE AS 陳述式)，使用憑證讓您得以利用追蹤找出預存程序的原始呼叫者。 這提供了更高層次的稽核，尤其是稽核安全性或資料定義語言 (DDL) 作業期間的一舉一動。  
  
您可以在 master 資料庫中建立憑證而賦予伺服器層級權限，或在任何使用者資料庫中建立憑證而賦予資料庫層級權限。 在此案例中，對基底資料表不具有權限的使用者必須存取 AdventureWorks2017 資料庫中的預存程序，而您則是希望稽核物件存取記錄。 您將不會用到其他的擁有權鏈結方法，而是要建立無權存取基底物件的伺服器和資料庫使用者帳戶，以及有權存取資料表和預存程序的資料庫使用者帳戶。 預存程序和第二個資料庫使用者帳戶都將由憑證提供安全性。 第二個資料庫帳戶可以存取所有物件，第一個資料庫使用者帳戶則僅獲授與存取預存程序。  
  
此案例會先建立資料庫憑證、預存程序和使用者，然後再測試程序，步驟依序如下：  
  
此範例會在每個程式碼區塊中各行附上說明。 若要複製整個範例，請參閱本教學課程結尾處的＜ [完整範例](#CompleteExample) ＞一節。  

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2017 sample databases](https://docs.microsoft.com/sql/samples/adventureworks-install-configure) (AdventureWorks2017 範例資料庫)。

如需還原 SQL Server Management Studio 中資料庫的指示，請參閱[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。   
  
## <a name="1-configure-the-environment"></a>1.設定環境  
為設定範例的初步內容，請在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中開啟新查詢，然後執行下列程式碼以開啟 Adventureworks2017 資料庫。 這段程式碼會將資料庫內容變更為 `AdventureWorks2012` ，再建立新的伺服器登入和資料庫使用者帳戶 (`TestCreditRatingUser`)，並且使用了密碼。  
  
```sql  
USE AdventureWorks2017;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
```  
  
如需 CREATE USER 陳述式的詳細資訊，請參閱 [CREATE USER &#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md)。 如需 CREATE LOGIN 陳述式的詳細資訊，請參閱 [CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md)。  
  
## <a name="2-create-a-certificate"></a>2.建立憑證  
您可以使用 master 資料庫、使用者資料庫或兩者做為內容，在伺服器中建立憑證。 保護憑證可用的選項有很多種。 如需憑證的詳細資訊，請參閱 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../t-sql/statements/create-certificate-transact-sql.md)。  
  
執行下列程式碼建立資料庫憑證，並且使用密碼保護該憑證。  
  
```sql  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2020';  -- Error 3701 will occur if this date is not in the future
GO  
```  
  
## <a name="3-create-and-sign-a-stored-procedure-using-the-certificate"></a>3.建立預存程序並使用憑證進行簽署  
使用下列程式碼來建立預存程序，此預存程序會從 `Vendor` 資料庫結構描述的 `Purchasing` 資料表中選取資料，以限制為只存取信用等級為 1 的公司。 請注意，預存程序的第一個區段會顯示執行預存程序之使用者帳戶的內容，這只能示範概念。 未必能滿足實際需求。  
  
```sql  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Show who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1  
END  
GO  
```  
  
執行下列程式碼，使用憑證加上密碼簽署預存程序。  
  
```sql  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
```  
  
如需預存程序的詳細資訊，請參閱[預存程序 &#40;Database Engine&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md)。  
  
如需簽署預存程序的詳細資訊，請參閱 [ADD SIGNATURE &#40;Transact-SQL&#41;](../t-sql/statements/add-signature-transact-sql.md)。  
  
## <a name="4-create-a-certificate-account-using-the-certificate"></a>4.使用憑證建立憑證帳戶  
執行下列程式碼，經由憑證建立資料庫使用者 (`TestCreditRatingcertificateAccount`)。 此帳戶不具有伺服器登入身分，最後將要用來控制基礎資料表的存取。  
  
```sql  
USE AdventureWorks2017;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="5-grant-the-certificate-account-database-rights"></a>5.授與憑證帳戶資料庫權限  
執行下列程式碼，授與 `TestCreditRatingcertificateAccount` 使用基底資料表和預存程序的權限。  
  
```sql  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
```  
  
如需授與物件權限的詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)。  
  
## <a name="6-display-the-access-context"></a>6.顯示存取內容  
為了顯示預存程序的相關存取權限，請執行下列程式碼授與 `TestCreditRatingUser` 使用者執行預存程序的權限。  
  
```sql  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
```  
  
接著執行下列程式碼，以便由您在伺服器上所用的 dbo 登入來執行預存程序。 觀察所輸出的使用者內容資訊。 顯示的結果將是 dbo 帳戶以其自身的權限執行而非透過群組成員資格。  
  
```sql  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
執行下列程式碼，使用 `EXECUTE AS` 陳述式改以 `TestCreditRatingUser` 帳戶身分來執行預存程序。 這回您會看到使用者內容已設定為 USER MAPPED TO CERTIFICATE 內容。  
  
```sql  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
這就達到了稽核目的，因為您已簽署過預存程序。  
  
> [!NOTE]  
> 使用 EXECUTE AS 可切換資料庫內的內容。  
  
## <a name="7-reset-the-environment"></a>7.重設環境  
下列程式碼使用 `REVERT` 陳述式，將目前帳戶的內容切換回 dbo 並重設環境。  
  
```sql  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
如需 REVERT 陳述式的詳細資訊，請參閱 [REVERT &#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md)。  
  
## <a name="CompleteExample"></a>完整範例  
本節顯示完整的範例程式碼。  
  
```sql  
/* Step 1 - Open the AdventureWorks2017 database */  
USE AdventureWorks2017;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
  
/* Step 2 - Create a certificate in the AdventureWorks2012 database */  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2020';   -- Error 3701 will occur if this date is not in the future
GO  
  
/* Step 3 - Create a stored procedure and  
sign it using the certificate */  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Shows who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token;     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1;  
END  
GO  
  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
  
/* Step 4 - Create a database user for the certificate.   
This user has the ownership chain associated with it. */  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
  
/* Step 5 - Grant the user database rights */  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE  
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
  
/* Step 6 - Test, using the EXECUTE AS statement */  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
  
-- Run the procedure as the dbo user, notice the output for the type  
EXEC TestCreditRatingSP;  
GO  
  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXEC TestCreditRatingSP;  
GO  
  
/* Step 7 - Clean up the example */  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  
