---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a7701edd4c1902399f1d040ae9027365bdf04ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997748"
---
# <a name="set-collate-command"></a>SET COLLATE 命令
在後續的索引和排序作業中，指定字元欄位的定序序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>引數  
 *cSequenceName*  
 指定定序序列。 下表描述可用的定序順序選項。  
  
|選項。|Language|  
|-------------|--------------|  
|荷蘭文|荷蘭文|  
|GENERAL|英文、法文、德文、新式西班牙文、葡萄牙文和其他西歐語言|  
|德語|德文的電話簿訂單（等）|  
|冰島|冰島文|  
|機器碼|電腦（舊版 FoxPro 版本的預設定序順序）|  
|NORDAN|挪威文，丹麥文|  
|西班牙文|傳統西班牙文|  
|SWEFIN|瑞典文、芬蘭文|  
|UNIQWT|唯一權數|  
  
> [!NOTE]  
>  當您指定西班牙文選項時， *ch*是在*c*和*d*之間排序的單一字母，而*ll*會在*l*和*m*之間排序。  
  
 如果您將定序序列選項指定為常值字元字串，請務必將選項括在引號中：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 [機器] 是預設定序順序選項，而且是使用者熟悉的序列 Xbase。 字元會依照出現在目前字碼頁中的順序排序。  
  
 一般適用于美國和西歐的使用者。 字元會依照出現在目前字碼頁中的順序排序。 在2.5 之前的 FoxPro 版本中，可能已經使用**大寫**（）或**LOWER**（）函數來建立索引，以將字元欄位轉換成一致的大小寫。 在2.5 以後的 FoxPro 版本中，您可以改為指定一般定序順序選項，並省略**上限**（）轉換。  
  
 如果您指定了電腦以外的定序順序選項，而且您建立了 idx 檔案，則一律會建立 compact. idx。  
  
 使用 SET （"COLLATE"）來傳回目前的定序序列。  
  
 您可以使用 [ [ODBC Visual FoxPro 安裝程式] 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)，或在連接字串中使用 Collate 關鍵字搭配[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)，為數據源指定排序次序。 這等同于發出下列命令：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>備註  
 [設定自動分頁] 可讓您針對任何支援的語言排序包含重音字元的資料表。 變更 SET COLLATE 的設定並不會影響先前開啟之索引的排序次序。 Visual FoxPro 會自動維護現有的索引，讓您可以彈性地建立許多不同類型的索引，即使是針對相同的欄位也一樣。  
  
 例如，如果建立的索引的設定 COLLATE 設定為 [一般]，而 SET COLLATE 設定稍後變更為 [西班牙文]，則索引會保留一般定序順序。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
