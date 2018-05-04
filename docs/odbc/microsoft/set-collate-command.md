---
title: SET COLLATE 命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a53941bc4b2ae95459d8f183a74736e17830d0a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-collate-command"></a>SET COLLATE 命令
指定字元欄位的定序順序中後續索引和排序作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引數  
 *cSequenceName*  
 指定定序序列。 下表將詳述可用的定序序列選項。  
  
|選項|語言|  
|-------------|--------------|  
|荷蘭文|荷蘭文|  
|GENERAL|英文、 法文、 德文、 現代西班牙文、 葡萄牙文和其他西歐語言|  
|德文|德文電話簿順序 (DIN)|  
|冰島|冰島文|  
|機器|電腦 （預設定序序列 FoxPro 舊版）|  
|NORDAN|挪威文、 丹麥文|  
|西班牙文|西班牙文|  
|SWEFIN|瑞典文、 芬蘭文|  
|UNIQWT|唯一的權數|  
  
> [!NOTE]  
>  當您指定西班牙文的選項， *ch*排序之間是單一字母*c*和*d*，和*ll*排序之間*l*和*m*。  
  
 如果您指定做為常值字元字串的定序順序選項，請務必以引號括住的選項：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 電腦是預設定序順序選項，且順序 Xbase 使用者很熟悉。 出現在目前的字碼頁排序字元。  
  
 一般可能較適合用於美國和西歐使用者。 出現在目前的字碼頁排序字元。 FoxPro 版本早於 2.5，索引可能已建立使用**上方**（) 或**低**（） 函式，以將字元欄位轉換成一致的情況。 FoxPro 版本晚於 2.5，您可以改為指定一般的定序順序選項，並省略**上方**（） 轉換。  
  
 如果您指定定序順序選項的電腦，如果您建立.idx 檔案以外，一定會建立壓縮.idx。  
  
 您可以使用 SET("COLLATE") 傳回目前的定序序列。  
  
 您可以使用指定的資料來源的定序順序[ODBC Visual FoxPro 安裝程式 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或在您使用的連接字串中使用 Collate 關鍵字[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。 這相當於發出下列命令：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>備註  
 設定自動分頁可讓您訂單資料表包含任何支援之語言的腔調的字元。 變更設定的設定定序不會影響先前開啟的索引定序順序。 Visual FoxPro 會自動維護現有的索引，提供彈性地建立許多不同類型的索引，即使為相同的欄位。  
  
 例如，如果索引建立設定定序設定為一般的設定自動分頁稍後在變更設定為西班牙文，索引會保留一般的定序序列。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
