---
title: 非系統地區設定 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: bd60bff3ab9ee19b1a1d2435e69651ea054689e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76913321"
---
# <a name="non-system-locale-settings"></a>非系統地區設定
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此節僅適用於 Linux 與 macOS 使用者，特別是在其 PHP 應用程式中處理多個地區設定的使用者。

根據預設，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會採用系統中定義的 `LC_ALL` 環境變數，並覆寫所有其他 `LC_xxx` 類別 (在某些情況下，可能除了 `$LANG` 或 `$LANGUAGE` 以外)，會影響千位分隔符號、小數點字元、字元集、月份、日期名稱、應用程式訊息 (如錯誤訊息、貨幣符號等)。

從 5.8.0 版開始，使用者可以使用 php .ini 檔案來設定當地語系化設定，如下列範例所示。

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>使用 SQLSRV 驅動程式設定地區設定資訊  
在 php.ini 檔案的結尾加入下列項目：
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>使用 PDO_SQLSRV 驅動程式設定地區設定資訊  
在 php.ini 檔案的結尾加入下列項目：
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
此**選項**可以是下列其中一個值：  
  
|選項|行為描述|
|---------|---------------|
|0|驅動程式會忽略系統地區設定。|
|1|驅動程式會讀取 LC_CTYPE 變數。|
|2|驅動程式會讀取 LC_ALL 變數 (這是預設值)。|
  

`LC_CTYPE` 類別會決定字元處理規則，該類別管理文字資料字元位元組序列的解釋、字元分類，以及字元類別的行為。 它會控制大寫和小寫、字母和非字母字元等的辨識。

### <a name="explanation"></a>說明

1. 選項 0 -- 當您不想要變更應用程式地區設定時，請使用此選項。

1. 選項 1 -- 使用此選項僅設定 `LC_CTYPE` 的系統值，而不會影響其他 `LC_xxx` 類別。

1. 選項 2 -- 使用 `LC_ALL` 覆寫所有 `LC_xxx` 類別，並影響 PHP 應用程式及其延伸模組。

如果任何 PHP 指令碼的地區設定與系統不同，您可能需要藉由呼叫 PHP 內建函式 [setlocale](https://www.php.net/manual/en/function.setlocale.php)，指定 PHP 指令碼中的地區設定。 

例如，如果系統預設值是 `en_US.UTF-8` 但 PHP 指令碼使用 `de_DE.UTF-8`，則請適當地呼叫 PHP 函式 `setlocale()`。

針對選項 2，只有在您的 PHP 指令碼與 `LC_ALL` 變數不同時，才會指出所需的地區設定。

> [!NOTE]
> 如果在 php.ini 中未定義任何內容，則目前的預設值是根據 `LC_ALL` 覆寫所有其他地區設定，而這將會**淘汰**。 在不久的將來，預設值是忽略系統地區設定。 因此，如果使用者想要保留目前的行為，則必須據以修改 php.ini 檔案。

如果 sqlsrv 和 pdo_sqlsrv 驅動程式都已啟用，則不建議為這兩個驅動程式設定不同的選項。