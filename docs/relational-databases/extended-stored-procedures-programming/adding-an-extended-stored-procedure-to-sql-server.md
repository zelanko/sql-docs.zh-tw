---
title: 將擴充預存程式加入至 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
author: rothja
ms.author: jroth
ms.openlocfilehash: bba543dbf89cb1dd3c0eb8a456a54c3c31c51d02
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67903414"
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>將擴充預存程序加入至 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 包含擴充預存程序的 DLL 會當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的延伸模組。 若要安裝 DLL，請將檔案複製到包含標準[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 檔案的目錄（C:\PROGRAM Files\Microsoft SQL Server\MSSQL12.0.*x*預設為 x \MSSQL\Binn）。  
  
 在擴充預存程序 DLL 已經複製到伺服器之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員必須向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊 DLL 中的每個擴充預存程序函數。 這項作業是使用 sp_addextendedproc 系統預存程序完成的。  
  
> [!IMPORTANT]  
>  系統管理員應該先徹底檢閱擴充預存程序，確定其中不含任何有害或惡意的程式碼，然後再將擴充預存程序加入至伺服器並將執行權限授與其他使用者。  驗證所有使用者輸入。 在使用者輸入完成驗證前，請勿加以串連。 請勿執行由未經驗證之使用者輸入所建構的命令。  
  
 sp_addextendedproc 的第一個參數會指定函數的名稱，而第二個參數會指定函數所在之 DLL 的名稱。 建議您指定 DLL 的完整路徑。  
  
> [!IMPORTANT]  
>  在升級到 SQL Server 2005 或更新版本之後，沒有用完整路徑註冊的現有 DLL 將無法運作。 若要更正這個問題，請利用 sp_dropextendedproc 來取消註冊 DLL，再利用 sp_addextendedproc 並指定完整路徑來重新註冊它。  
  
 在 `sp_addextendedproc` 中指定的函數名稱必須與 DLL 中的函數名稱完全相同 (包括大小寫)。 例如，此命令會註冊 `xp_hello,` 函數 (位於名為 `xp_hello.dll` 的 dll 中) 當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴充預存程序：  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL13.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 如果在 `sp_addextendedproc` 中指定的函數名稱並未與 DLL 中的函數名稱完全相符，系統將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中註冊新名稱，但是此名稱將無法使用。 例如，雖然會`xp_Hello`註冊為位於的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]擴充預存程式`xp_hello.dll`，但[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果您稍後使用`xp_Hello`呼叫函式，將無法在 DLL 中找到該函式。  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 如果在 `sp_addextendedproc` 中指定的函數名稱與 DLL 中的函數名稱完全相符，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的定序不會區分大小寫，使用者就可以使用名稱的任何大小寫字母組合來呼叫此擴充預存程序。  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的定序會區分大小寫時，如果使用不同的大小寫來呼叫此擴充預存程序，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就無法呼叫此擴充預存程序，即使它使用完全相同的名稱和定序註冊成 DLL 中的函數也一樣。  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 您不需要停止並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
