---
title: '@@OPTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e33ca6d8afdb7aa9245bbdc6b0ad225dcd00dade
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "73982466"
---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;OPTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前 SET 選項的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>傳回型別  
 **integer**  
  
## <a name="remarks"></a>備註  
 選項可來自於 **SET** 命令，或來自 **sp_configure user options** 值。 以 **SET** 命令設定的工作階段值會覆寫 **sp_configure** 選項。 許多工具 (例如 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) 會自動設定 set 選項。 每位使用者都有一個代表設定的 @@OPTIONS 函式。  
  
 您可以利用 SET 陳述式來變更特定使用者工作階段的語言和查詢處理選項。 **\@\@OPTIONS** 只能偵測設為 ON 或 OFF 的選項。  
  
 **\@\@OPTIONS** 函式會傳回選項的點陣圖，並轉換成以 10 為底數 (十進位) 的整數。 位元設定會儲存在[設定 user options 伺服器設定選項](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)主題中資料表內描述的位置裡。  
  
 若要解碼 **\@\@OPTIONS** 值，請將 **\@\@OPTIONS** 傳回的整數轉換為二進位，然後在[設定使用者選項伺服器設定選項](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)的資料表中查詢該值。 例如，若 `SELECT @@OPTIONS;` 傳回值 `5496`，請使用 Windows 工程型小算盤 (**calc.exe**) 將十進位 `5496` 轉換成二進位。 結果為 `1010101111000`。 最右邊的字元 (二進位 1、2 及 4) 為 0，表示資料表中的前三個項目為關閉 (off)。 查閱資料表，您會看到它們為 **DISABLE_DEF_CNST_CHK**、**IMPLICIT_TRANSACTIONS** 和 **CURSOR_CLOSE_ON_COMMIT**。 下一個項目 (`1000` 位置中的 **ANSI_WARNINGS**) 為開啟 (on)。 在位元對應中繼續向左，然後在選項清單中向下。 當最左邊的選項為 0 時，就會被類型轉換截斷。 點陣圖 `1010101111000` 實際上是 `001010101111000` 來表示所有 15 個選項。  
  
## <a name="examples"></a>範例  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. 變更影響行為的示範  
 下列範例示範兩個不同 **CONCAT_NULL_YIELDS_NULL** 選項的設定，導致串連行為的差異。  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. 測試用戶端 NOCOUNT 設定  
 下列範例會設定 `NOCOUNT``ON`，然後測試 `@@OPTIONS` 的值。 `NOCOUNT``ON` 選項會防止針對工作階段中的每個陳述式，將受影響之資料列數的相關訊息傳回發出要求的用戶端。 `@@OPTIONS` 值設為 `512` (0x0200)。 這代表 NOCOUNT 選項。 這個範例會測試是否啟用了用戶端的 NOCOUNT 選項。 例如，它可以協助您追蹤用戶端的效能差異。  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [設定使用者選項伺服器組態選項](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
