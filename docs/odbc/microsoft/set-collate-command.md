---
title: 設定 COLLATE 命令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9c1dfd59c00ad0ac0b7bd8b8f1cdfccc84d9b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300888"
---
# <a name="set-collate-command"></a>SET COLLATE 命令
為後續索引和排序操作中字元欄位指定排序序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引數  
 *c 序列名稱*  
 指定排序規則序列。 下表描述了可用的排序規則選項。  
  
|選項。|Language|  
|-------------|--------------|  
|荷蘭文|荷蘭文|  
|GENERAL|英語、法語、德語、現代西班牙文、葡萄牙文和其他西歐語言|  
|德語|德國電話簿訂單 (DIN)|  
|冰島|冰島文|  
|機|電腦(早期 FoxPro 版本的預設排序規則序列)|  
|諾丹|挪威語, 丹麥文|  
|西班牙文|傳統西班牙文|  
|斯威芬|瑞典語, 芬蘭文|  
|優衣庫|獨特的重量|  
  
> [!NOTE]  
>  指定 SPANISH 選項時 *,ch*是一個字母,在*c*和*d*之間排序,*並在* *l*和*m*之間排序。  
  
 如果將排序規則序列選項指定為文字字串,請確保在引號中包含這個選項:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE 是預設排序規則序列選項,是 Xbase 使用者熟悉的序列。 字元在目前的程式碼頁中顯示時進行排序。  
  
 對於美國和西歐用戶來說,GENERAL 可能更可取。 字元在目前的程式碼頁中顯示時進行排序。 在 FoxPro 版本早於 2.5 中,索引可能已使用**上部**( ) 或**LOWER**( ) 函數創建,以將字元欄位轉換為一致大小寫。 在 FoxPro 版本晚於 2.5 中,您可以改為指定 GENERAL 排序規則序列選項並省略**UPPER**( ) 轉換。  
  
 如果指定「機器」以外的排序規則序列選項,並且如果創建 .idx 檔,則始終創建緊湊的 .idx。  
  
 使用 SET("COLLATE")傳回目前排序規則序列。  
  
 您可以使用[ODBC 視覺化 FoxPro 安裝程式對話框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或使用與[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)的連接字串中的「Collate 關鍵字」為資料源指定整理序列。 這與發出以下指令相同:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>備註  
 SET COLLATE 使您能夠為任何受支援的語言訂購包含重音字元的表。 更改 SET COLLATE 的設定不會影響以前打開的索引的整理順序。 Visual FoxPro 可自動維護現有索引,從而靈活地創建許多不同類型的索引,即使對於同一字段也是如此。  
  
 例如,如果使用 SET COLLATE 設置為「GENERAL」建立索引,並且「設定 COLLATE」設定稍後更改為西班牙文,則索引將保留「常規排序規則」 序列。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
