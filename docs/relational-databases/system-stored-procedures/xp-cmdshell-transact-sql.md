---
title: xp_cmdshell (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 73609eae141fd96f9a2f01bccc3cf18347a0fc00
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262921"
---
# <a name="xpcmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  繁衍 Windows 命令 Shell 並傳入字串中以供執行。 任何輸出都會當作文字資料列來傳回。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>引數  
 **'** *command_string* **'**  
 這是包含要傳送至作業系統之命令的字串。 *command_string*是**varchar(8000)** 或**nvarchar （4000)**，沒有預設值。 *command_string*不能包含多組雙引號括住。 如果檔案路徑中有任何空格，或參考的程式名稱，則需要一對引號*command_string*。 如果使用內嵌空格會出錯，請考慮改用 FAT 8.3 檔案名稱作為因應措施。  
  
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
  
 資料列的傳回**nvarchar （255)** 資料行。 如果**no_output**使用選項，只有下列將會傳回：  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>備註  
 Windows 處理序所繁衍**xp_cmdshell**具有相同的安全性權限，為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶。  
  
 **xp_cmdshell**以同步方式運作。 完成 command-shell 命令時，才會將控制權傳回呼叫端。  
  
 **xp_cmdshell**可以啟用和停用使用以原則為基礎的管理，或藉由執行**sp_configure**。 如需詳細資訊，請參閱[介面區組態](../../relational-databases/security/surface-area-configuration.md)和[xp_cmdshell 伺服器組態選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
> [!IMPORTANT]  
>  如果**xp_cmdshell**批次內執行時，並傳回錯誤，批次將會失敗。 這是行為的變更。 在舊版的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]批次會繼續執行。  
  
## <a name="xpcmdshell-proxy-account"></a>xp_cmdshell Proxy 帳戶  
 呼叫此方法不是成員的使用者當**sysadmin**固定伺服器角色、 **xp_cmdshell**來使用的帳戶名稱和密碼儲存在名為的認證連接到 Windows **# #xp_cmdshell_proxy_account # #**。 如果這個 proxy 認證不存在， **xp_cmdshell**將會失敗。  
  
 您可以建立 proxy 帳戶認證執行**sp_xp_cmdshell_proxy_account**。 作為引數，這個預存程序會取得 Windows 使用者名稱和密碼。 例如，下列命令會針對 Windows 網域使用者 `SHIPPING\KobeR` (這個使用者有 Windows 密碼 `sdfh%dkc93vcMt0`) 來建立 Proxy 認證。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 如需詳細資訊，請參閱[sp_xp_cmdshell_proxy_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 因為惡意使用者有時會嘗試藉由提高其權限**xp_cmdshell**， **xp_cmdshell**預設會停用。 使用**sp_configure**或**原則式管理**加以啟用。 如需詳細資訊，請參閱 [xp_cmdshell 伺服器組態選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 第一次啟用時， **xp_cmdshell**需要 CONTROL SERVER 權限來執行與所建立的 Windows 處理序**xp_cmdshell**具有相同的安全性內容，做為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶通常會有比所需的建立程序所執行之工作的權限**xp_cmdshell**。 為了加強安全性，存取**xp_cmdshell**應該限制為高權限使用者。  
  
 若要允許非系統管理員使用**xp_cmdshell**，並允許[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要建立子處理程序與較低權限帳戶的安全性權杖，請遵循下列步驟：  
  
1.  使用您的處理序所需的最低權限，建立及自訂 Windows 本機使用者帳戶或是網域帳戶。  
  
2.  使用**sp_xp_cmdshell_proxy_account**系統程序來設定**xp_cmdshell**使用該最低權限帳戶。  
  
    > [!NOTE]  
    >  您也可以設定此 proxy 帳戶使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]以滑鼠右鍵按一下**屬性**伺服器名稱上的 [物件總管] 中，並查看 [**安全性**] 索引標籤**伺服器proxy 帳戶**> 一節。  
  
3.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，使用 master 資料庫，執行`GRANT exec ON xp_cmdshell TO '<somelogin>'`陳述式，提供特定非**sysadmin**使用者執行的能力**xp_cmdshell**。 指定的登入必須對應到 master 資料庫中的使用者。  
  
 非系統管理員可以啟動作業系統處理程序與現在**xp_cmdshell**和已設定的 proxy 帳戶的權限執行這些程序。 具有 CONTROL SERVER 權限的使用者 (成員**sysadmin**固定的伺服器角色) 將繼續接收的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務所啟動的子處理序帳戶**xp_cmdshell**.  
  
 若要判斷所使用的 Windows 帳戶**xp_cmdshell**時啟動作業系統處理序，執行下列陳述式：  
  
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
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>B. 未傳回輸出  
 下列範例會利用 `xp_cmdshell` 執行命令字串，但不將輸出傳回用戶端。  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>C. 使用傳回狀態  
 在下列範例中，`xp_cmdshell`擴充預存程序也建議傳回狀態。 傳回碼值儲存在變數 `@result` 中。  
  
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
 [一般擴充預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell 伺服器組態選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [介面區組態](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
