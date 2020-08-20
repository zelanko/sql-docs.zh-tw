---
description: SET COLLATE 命令
title: 設定 COLLATE 命令 |Microsoft Docs
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
ms.openlocfilehash: 5ca796da60adf0c432b5bbd80065e58563664bc5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466380"
---
# <a name="set-collate-command"></a>SET COLLATE 命令
在後續的索引和排序作業中，指定字元欄位的定序序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引數  
 *cSequenceName*  
 指定定序序列。 下表說明可用的定序順序選項。  
  
|選項。|Language|  
|-------------|--------------|  
|荷蘭文|荷蘭文|  
|GENERAL|英文、法文、德文、新式西班牙文、葡萄牙文和其他西歐語言|  
|德語|德國行動電話簿訂單 (的) |  
|冰島|冰島文|  
|機|電腦 (舊版 FoxPro 版本的預設定序順序) |  
|NORDAN|挪威文（丹麥文）|  
|西班牙文|傳統西班牙文|  
|SWEFIN|瑞典文、芬蘭文|  
|UNIQWT|唯一權數|  
  
> [!NOTE]  
>  當您指定西班牙文選項時， *ch*是在*c*和*d*之間排序的單一字母，而會在*l*和*m**之間進行排序*。  
  
 如果您將定序序列選項指定為常值字元字串，請務必將選項括在引號中：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 [機器] 是預設的定序順序選項，也是使用者熟悉的序列 Xbase。 字元會依出現在目前字碼頁中的順序排序。  
  
 美國和西歐使用者可能會偏好一般。 字元會依出現在目前字碼頁中的順序排序。 在2.5 之前的 FoxPro 版本中，可能已使用 **上方** ( ) 或 **較低** 的 ( ) 函式來建立索引，以將字元欄位轉換為一致的大小寫。 在 FoxPro 2.5 以後的版本中，您可以改為指定 [一般定序順序] 選項，並省略 ) 轉換的 **上方** (。  
  
 如果您指定的是 [電腦以外的定序順序] 選項，而且建立 idx 檔案，一律會建立 compact. idx。  
  
 使用 SET ( "COLLATE" ) 來傳回目前的定序序列。  
  
 您可以使用 [ [ODBC Visual FoxPro 安裝程式] 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ，或在連接字串中使用 Collate 關鍵字搭配 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)，以指定資料來源的排序次序。 這等同于發出下列命令：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>備註  
 SET COLLATE 可讓您排序包含任何支援語言之重音字元的資料表。 變更 SET COLLATE 的設定不會影響先前開啟之索引的排序次序。 Visual FoxPro 會自動維護現有的索引，讓您可以彈性地建立許多不同類型的索引，即使是相同的欄位也一樣。  
  
 例如，如果建立索引時將 SET COLLATE 設定為 [一般]，而 [設定定序] 設定稍後變更為西班牙文，則索引會保留一般定序順序。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
