---
description: xp_cmdshell (Transact-SQL)
title: xp_cmdshell (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3333e8d26c6f79bc3f99298e2854f05789caac9f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541013"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  繁衍 Windows 命令 Shell 並傳入字串中以供執行。 任何輸出都會當作文字資料列來傳回。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>引數  
 **'** *command_string* **'**  
 這是包含要傳送至作業系統之命令的字串。 *command_string* 是 **Varchar (8000) ** 或 **Nvarchar (4000) **，沒有預設值。 *command_string* 不能包含一組以上的雙引號。 如果 *command_string*中參考的檔案路徑或程式名稱中有任何空格，則需要一對引號。 如果使用內嵌空格會出錯，請考慮改用 FAT 8.3 檔案名稱作為因應措施。  
  
 **no_output**  
 這是選擇性參數，用來指定不應將輸出傳回用戶端。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 執行下列 `xp_cmdshell` 陳述式會傳回目前目錄的目錄清單。  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 資料列會在 **Nvarchar (255) ** 資料行中傳回。 如果使用 **no_output** 選項，則只會傳回下列各項：  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>備註  
 **Xp_cmdshell**所產生的 Windows 進程具有與服務帳戶相同的安全性許可權 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **xp_cmdshell** 會以同步方式運作。 完成 command-shell 命令時，才會將控制權傳回呼叫端。  
  
 您可以使用以原則為基礎的管理或執行**sp_configure**來啟用和停用**xp_cmdshell** 。 如需詳細資訊，請參閱 [介面區](../../relational-databases/security/surface-area-configuration.md) 設定和 [Xp_cmdshell Server configuration 選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
> [!IMPORTANT]
>  如果在批次內執行 **xp_cmdshell** ，並傳回錯誤，批次將會失敗。 這是行為的變更。 在較舊版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 批次中，將會繼續執行。  
  
## <a name="xp_cmdshell-proxy-account"></a>xp_cmdshell Proxy 帳戶  
 當使用者呼叫的使用者不是 **系統管理員（sysadmin** ）固定伺服器角色的成員時， **xp_cmdshell** 會使用儲存在名為 **# #xp_cmdshell_proxy_account # #** 的認證中的帳戶名稱和密碼來連接到 Windows。 如果此 proxy 認證不存在， **xp_cmdshell** 將會失敗。  
  
 您可以藉由執行 **sp_xp_cmdshell_proxy_account**來建立 proxy 帳號憑證。 作為引數，這個預存程序會取得 Windows 使用者名稱和密碼。 例如，下列命令會針對 Windows 網域使用者 `SHIPPING\KobeR` (這個使用者有 Windows 密碼 `sdfh%dkc93vcMt0`) 來建立 Proxy 認證。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 如需詳細資訊，請參閱 [sp_xp_cmdshell_proxy_account &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 由於惡意使用者有時候會使用 **xp_cmdshell**來嘗試提高其許可權，因此預設會停用 **xp_cmdshell** 。 使用 **sp_configure** 或以 **原則為基礎的管理** 來啟用它。 如需詳細資訊，請參閱 [xp_cmdshell 伺服器組態選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 第一次啟用時， **xp_cmdshell** 需要 CONTROL SERVER 許可權才能執行，而且 **xp_cmdshell** 所建立的 Windows 進程具有與服務帳戶相同的安全性內容 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶通常會有比**xp_cmdshell**所建立的進程所執行的工作更多的許可權。 為了加強安全性， **xp_cmdshell** 的存取權應該限制為具有高許可權的使用者。  
  
 若要允許非系統管理員使用 **xp_cmdshell**，並允許使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 較低許可權帳戶的安全性權杖來建立子進程，請遵循下列步驟：  
  
1.  使用您的處理序所需的最低權限，建立及自訂 Windows 本機使用者帳戶或是網域帳戶。  
  
2.  使用 **sp_xp_cmdshell_proxy_account** 系統程式，將 **xp_cmdshell** 設定為使用該最低許可權的帳戶。  
  
    > [!NOTE]  
    >  您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 滑鼠右鍵按一下物件總管中伺服器名稱的**Properties** [內容]，然後查看 [**伺服器 proxy 帳戶**] 區段的 [**安全性**] 索引標籤，來設定此 proxy 帳戶。  
  
3.  在中 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ，使用 master 資料庫執行語句，為 `GRANT exec ON xp_cmdshell TO N'<some_user>';` 特定的非**系統管理員** 使用者提供執行 **xp_cmdshell**的能力。 指定的使用者必須存在於 master 資料庫中。  
  
 現在，非系統管理員可以使用 **xp_cmdshell** 啟動作業系統進程，而這些進程會以您已設定之 proxy 帳戶的許可權來執行。 具有 CONTROL SERVER 許可權 (**系統管理員（sysadmin** ）固定伺服器角色成員的使用者) 將繼續接收 xp_cmdshell 所 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動之子進程的服務帳戶許可權。 **xp_cmdshell**  
  
 若要判斷 **xp_cmdshell** 啟動作業系統進程時所使用的 Windows 帳戶，請執行下列語句：  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 若要判斷另一個登入的安全性內容，請執行下列程式碼：  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. 傳回可執行檔清單  
 下列範例會顯示執行目錄命令的 `xp_cmdshell` 擴充預存程序。  
  
```  
EXEC master..xp_cmdshell 'dir *.exe'  
```  
  
### <a name="b-returning-no-output"></a>B. 未傳回輸出  
 下列範例會利用 `xp_cmdshell` 執行命令字串，但不將輸出傳回用戶端。  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks', NO_OUTPUT;  
GO  
```  
  
### <a name="c-using-return-status"></a>C. 使用傳回狀態  
 在下列範例中， `xp_cmdshell` 擴充預存程式也會建議傳回狀態。 傳回碼值儲存在變數 `@result` 中。  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. 將變數內容寫入檔案  
 下列範例將 `@var` 變數的內容寫入目前伺服器目錄中一個命名為 `var_out.txt` 的檔案。  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. 將命令結果擷取至檔案  
 下列範例會將目前目錄的內容寫入目前伺服器目錄中一個名稱為 `dir_out.txt` 的檔案。  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的一般擴充預存程式 ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell 伺服器設定選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [介面區組態](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
