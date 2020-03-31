---
title: xp_cmdshell（轉算-SQL） |微軟文檔
ms.custom: ''
ms.date: 03/30/2020
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2ce32fc31373077418e77d31ce064d60e23f1b24
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402696"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  繁衍 Windows 命令 Shell 並傳入字串中以供執行。 任何輸出都會當作文字資料列來傳回。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>引數  
 **'** *command_string* **'**  
 這是包含要傳送至作業系統之命令的字串。 *command_string*是**瓦爾查爾（8000）** 或**Nvarchar（4000），** 沒有違約。 *command_string*不能包含一組以上的雙引號。 如果檔路徑或*command_string*引用的程式名稱中存在任何空格，則需要一對引號。 如果使用內嵌空格會出錯，請考慮改用 FAT 8.3 檔案名稱作為因應措施。  
  
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
  
 行在**Nvarchar（255）** 列中返回。 如果使用**no_output**選項，則僅返回以下內容：  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>備註  
 **xp_cmdshell**生成的 Windows 進程具有與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶相同的安全許可權。  
  
 **xp_cmdshell**同步運行。 完成 command-shell 命令時，才會將控制權傳回呼叫端。  
  
 xp_cmdshell**可以通過使用**基於策略的管理或執行**sp_configure**啟用和禁用。 有關詳細資訊，請參閱[曲面區域配置](../../relational-databases/security/surface-area-configuration.md)[和xp_cmdshell伺服器配置選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
> [!IMPORTANT]
>  如果在批次處理中執行**xp_cmdshell**並返回錯誤，則批次處理將失敗。
  
## <a name="xp_cmdshell-proxy-account"></a>xp_cmdshell Proxy 帳戶  
 當它不是**sysadmin**固定伺服器角色的成員的使用者調用它時 **，xp_cmdshell**使用存儲在名為 **[#xp_cmdshell_proxy_account]** 的憑據中的帳戶名稱和密碼連接到 Windows。 如果此代理憑據不存在 **，xp_cmdshell**將失敗。  
  
 代理帳戶憑據可以通過執行**sp_xp_cmdshell_proxy_account**創建。 作為引數，這個預存程序會取得 Windows 使用者名稱和密碼。 例如，下列命令會針對 Windows 網域使用者 `SHIPPING\KobeR` (這個使用者有 Windows 密碼 `sdfh%dkc93vcMt0`) 來建立 Proxy 認證。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 有關詳細資訊，請參閱[sp_xp_cmdshell_proxy_account&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 由於惡意使用者有時嘗試使用**xp_cmdshell**來提升其特權，因此預設情況下將禁用**xp_cmdshell。** 使用**sp_configure**或**基於策略的管理**啟用它。 如需詳細資訊，請參閱 [xp_cmdshell 伺服器組態選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 首次啟用時 **，xp_cmdshell**需要執行控制伺服器許可權，**並且xp_cmdshell**創建的 Windows 進程具有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與服務帳戶相同的安全上下文。 服務[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]帳戶通常具有比**xp_cmdshell**創建的進程執行的工作所需的許可權更多。 為了提高安全性，應限制對**xp_cmdshell**的訪問僅限於高特權使用者。  
  
 要允許非管理員使用**xp_cmdshell**，並允許[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用許可權較低的帳戶的安全權杖創建子進程，請按照以下步驟操作：  
  
1.  使用您的處理序所需的最低權限，建立及自訂 Windows 本機使用者帳戶或是網域帳戶。  
  
2.  使用**sp_xp_cmdshell_proxy_account**系統過程配置**xp_cmdshell**以使用該最低許可權的帳戶。  
  
    > [!NOTE]  
    >  您還可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**右鍵**按一下物件資源管理器中的伺服器名稱的屬性，以及查看**伺服器代理帳戶****部分的安全選項卡**來配置此代理帳戶。  
  
3.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中使用主資料庫執行`GRANT exec ON xp_cmdshell TO N'<some_user>';`語句，使特定的非**系統管理員**使用者能夠執行**xp_cmdshell**。 指定的使用者必須存在於主資料庫中。  
  
 現在，非管理員可以使用**xp_cmdshell**啟動作業系統進程，這些進程使用您配置的代理帳戶的許可權運行。 具有 CONTROL SERVER 許可權的使用者 **（sysadmin**固定伺服器角色的成員）將繼續接收**xp_cmdshell**啟動[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的子進程的服務帳戶的許可權。  
  
 要確定**xp_cmdshell**在啟動作業系統進程時使用的 Windows 帳戶，請執行以下語句：  
  
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
 在下面的示例中，擴展的`xp_cmdshell`預存程序還建議返回狀態。 傳回碼值儲存在變數 `@result` 中。  
  
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
 [&#40;處理-SQL&#41;的一般擴充預存程序](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell伺服器配置選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [表面積配置](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
