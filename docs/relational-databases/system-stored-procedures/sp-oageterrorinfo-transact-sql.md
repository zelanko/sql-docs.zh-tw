---
description: sp_OAGetErrorInfo (Transact-SQL)
title: sp_OAGetErrorInfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 89bb7dff2131d8463e26754148aa6e8032503fd7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546000"
---
# <a name="sp_oageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  取得 OLE Automation 錯誤資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>引數  
 *objecttoken*  
 這是先前使用 **sp_OACreate** 所建立之 OLE 物件的物件 token，或是 Null。 如果指定 *objecttoken* ，則會傳回該物件的錯誤資訊。 如果指定了 NULL，就會傳回整個批次的錯誤資訊。  
  
 _來源_**輸出**  
 這是錯誤資訊的來源。 如果指定的話，它必須是本機 **char**、 **Nchar**、 **Varchar**或 **Nvarchar** 變數。 必要的話，會截斷傳回值來配合本機變數。  
  
 _描述_**輸出**  
 這是錯誤的描述。 如果指定的話，它必須是本機 **char**、 **Nchar**、 **Varchar**或 **Nvarchar** 變數。 必要的話，會截斷傳回值來配合本機變數。  
  
 _説明_的 **輸出**  
 這是 OLE 物件的說明檔。 如果指定的話，它必須是本機 **char**、 **Nchar**、 **Varchar**或 **Nvarchar** 變數。 必要的話，會截斷傳回值來配合本機變數。  
  
 _h_ **輸出**  
 這是說明檔案內容識別碼。 如果指定的話，它必須是本機 **int** 變數。  
  
> [!NOTE]  
>  這個預存程序的參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需 HRESULT 傳回碼的詳細資訊，請參閱 [OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>結果集  
 如果未指定輸出參數，就會將錯誤資訊當作結果集傳回給用戶端。  
  
|資料行名稱|資料類型|描述|  
|------------------|---------------|-----------------|  
|**錯誤**|**二元 (4) **|錯誤號碼的二進位表示法。|  
|**Source**|**Nvarchar (nn) **|錯誤的來源。|  
|**說明**|**Nvarchar (nn) **|錯誤的描述。|  
|**Helpfile**|**Nvarchar (nn) **|來源的說明檔。|  
|**HelpID**|**int**|說明來源檔案中的說明內容識別碼。|  
  
## <a name="remarks"></a>備註  
 每次呼叫 OLE Automation 預存程式 (但 **sp_OAGetErrorInfo**) 會重設錯誤資訊;因此， **sp_OAGetErrorInfo** 只會取得最新 OLE Automation 預存程序呼叫的錯誤資訊。 請注意，因為 **sp_OAGetErrorInfo** 不會重設錯誤資訊，所以可以多次呼叫，以取得相同的錯誤資訊。  
  
 下表列出 OLE Automation 錯誤及其共同原因。  
  
|錯誤和 HRESULT|共同原因|  
|-----------------------|------------------|  
|**不正確的變數類型 (0x80020008)**|做 [!INCLUDE[tsql](../../includes/tsql-md.md)] 為方法參數傳遞之值的資料類型不符合 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 方法參數的資料類型，或傳遞 Null 值做為方法參數。|  
|**未知名稱 (0x8002006)**|找不到指定物件的指定屬性或方法名稱。|  
|**無效的類別字串 (0x800401f3)**|指定的 ProgID 或 CLSID 未登錄為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 OLE 物件。 自訂 OLE automation 伺服器必須先註冊，才能使用 **sp_OACreate**具現化。 您可以使用同進程 ( .dll) 伺服器的 Regsvr32.exe 公用程式，或本機 ( .exe) 伺服器的 **/REGSERVER** 命令列參數來完成這項作業。|  
|**伺服器執行失敗 (0x80080005)**|指定的 OLE 物件已登錄成本機 OLE 伺服器 (.exe 檔)，但找不到或無法啟動 .exe 檔。|  
|**找不到指定的模組 (0x8007007e)**|指定的 OLE 物件已登錄成同處理序 OLE 伺服器 (.dll 檔)，但找不到或無法載入 .dll 檔。|  
|**類型不符 (0x80020005)**|用來儲存傳回的屬性值或方法傳回值之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 本機變數的資料類型不符合屬性或方法傳回值的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 資料類型。 或要求了屬性或方法的傳回值，但它沒有傳回值。|  
|**Sp_OACreate 的 ' coNtext ' 參數的資料類型或值無效。 (0x8004275B) **|context 參數的值應該是下列項目之一：1、4 或 5。|  
  
 如需處理 HRESULT 傳回碼的詳細資訊，請參閱 [OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或直接在此預存程式上執行許可權。 `Ole Automation Procedures` 必須 **啟用** 設定，才能使用任何與 OLE Automation 相關的系統程式。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 OLE Automation 錯誤資訊。  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>另請參閱  
 [OLE Automation 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
