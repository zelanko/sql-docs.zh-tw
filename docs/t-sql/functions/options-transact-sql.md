---
title: "@@OPTIONS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 9480ffeffa83650b5cf44ad51547c36d5563b13b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40; 選項 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前 SET 選項的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 選項可來自使用**設定**命令或從**sp_configure 使用者選項**值。 使用設定的工作階段值**設定**命令覆寫**sp_configure**選項。 許多工具 (例如 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) 會自動設定 set 選項。 每個使用者擁有 @@OPTIONS代表設定的函式。  
  
 您可以利用 SET 陳述式來變更特定使用者工作階段的語言和查詢處理選項。 **@@OPTIONS** 只能偵測的選項設定為 ON 或 OFF。  
  
 **@@OPTIONS** 函式會傳回選項，並轉換成基底 10 （十進位） 的整數的點陣圖。 位元設定會儲存在本主題中的資料表中所述的位置[設定 user options 伺服器組態選項](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)。  
  
 要解碼**@@OPTIONS** 值時，所傳回的整數轉換**@@OPTIONS** 為二進位，然後在資料表上的值查詢[設定 user options 伺服器組態選項](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)。 例如，如果`SELECT @@OPTIONS;`傳回的值`5496`，使用 Windows 工程型小算盤 (**calc.exe**) 要轉換的十進位`5496`二進位檔。 結果為 `1010101111000`。 右大部分字元 （二進位 1、 2 和 4） 都是 0，表示資料表中的前三個項目已關閉。 查閱資料表，您會看到這些是**DISABLE_DEF_CNST_CHK**和**IMPLICIT_TRANSACTIONS**，和**CURSOR_CLOSE_ON_COMMIT**。 下一個項目 (**ANSI_WARNINGS**中`1000`位置) 上。 繼續透過使用左位元對應中，並在選項清單中向下。 0 的最左邊的選項時，它們會被截斷的類型轉換。 點陣圖 `1010101111000` 實際上是 `001010101111000` 來表示所有 15 個選項。  
  
## <a name="examples"></a>範例  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. 變更影響行為的示範  
 下列範例會示範兩個不同的值為串連行為的差異**CONCAT_NULL_YIELDS_NULL**選項。  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. 測試用戶端 NOCOUNT 設定  
 下列範例會設定`NOCOUNT``ON`然後測試的值`@@OPTIONS`。 `NOCOUNT``ON`選項會阻止傳送回要求的用戶端工作階段中的每一個陳述式影響的資料列數目的相關訊息。 `@@OPTIONS` 值設為 `512` (0x0200)。 這代表 NOCOUNT 選項。 這個範例會測試是否啟用了用戶端的 NOCOUNT 選項。 例如，它可以協助您追蹤用戶端的效能差異。  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [設定使用者選項伺服器組態選項](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  

