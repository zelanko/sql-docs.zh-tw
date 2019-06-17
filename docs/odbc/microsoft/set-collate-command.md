---
title: SET COLLATE 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 372d3b2df79d66084f5599b4ac098b8c273ee78a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127837"
---
# <a name="set-collate-command"></a>SET COLLATE 命令
在後續的編製索引和排序作業中指定字元欄位的定序順序。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引數  
 *cSequenceName*  
 指定定序序列。 下表詳述可用的定序序列選項。  
  
|選項。|語言|  
|-------------|--------------|  
|荷蘭文|荷蘭文|  
|GENERAL|英文、 法文、 德文、 現代的西班牙文、 葡萄牙文和其他西歐語言|  
|德文|德文電話簿順序 (DIN)|  
|冰島|冰島文|  
|機器|機器 （預設定序序列較舊的 FoxPro 版本）|  
|NORDAN|挪威文、 丹麥文|  
|西班牙文|西班牙文|  
|SWEFIN|瑞典文、 芬蘭文|  
|UNIQWT|唯一的權數|  
  
> [!NOTE]  
>  當您指定西班牙文的選項， *ch*排序之間的單一字母*c*並*d*，並*ll*之間排序*l*並*m*。  
  
 如果您指定為常值字元字串的定序順序選項，請務必以引號括住的選項：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 是預設定序順序選項，順序 Xbase 使用者熟悉機器。 出現在目前的字碼頁排序字元。  
  
 一般可能會偏好美國和歐洲西部的使用者使用。 出現在目前的字碼頁排序字元。 FoxPro 版本早於 2.5 中，索引可能已建立使用**上方**（) 或**低**（） 函數，將字元欄位轉換成一致的大小寫。 FoxPro 版本晚於 2.5，可以改為指定一般的定序順序選項，並省略**上方**（） 轉換。  
  
 如果您指定機器 」 和 「 如果您建立.idx 檔案以外的定序順序選項，則一律會建立 compact.idx。  
  
 您可以使用 SET("COLLATE")，傳回目前的定序序列。  
  
 您可以使用，以指定的資料來源的定序順序[ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或您使用的連接字串中使用 Collate 關鍵字[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。 這等同於發出下列命令：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>備註  
 設定定序可讓您訂單資料表包含加重音的字元，任何支援的語言。 變更設定定序的設定不會影響先前開啟的索引定序順序。 Visual FoxPro 會自動維護現有的索引，進而有彈性地建立許多不同類型的索引，甚至是相同的欄位。  
  
 比方說，如果索引建立與設定定序設定為 一般設定定序設定於之後變更為西班牙文，則索引會保留一般的定序序列。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
