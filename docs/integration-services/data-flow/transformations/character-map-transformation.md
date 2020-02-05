---
title: 字元對應轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8211045a72ae56b04bb93b7be7e83f296f2467e5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71291660"
---
# <a name="character-map-transformation"></a>字元對應轉換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「字元對應」轉換會套用字串函數，例如從小寫轉換成大寫、字元資料。 此轉換只能在字串資料類型的資料行資料上操作。  
  
 「字元對應」轉換可就地轉換資料行資料，或將資料行加入至轉換輸出，並將轉換的資料放入新的資料行。 您可以將不同組的對應作業套用至同一輸入資料行，並將結果放入不同的資料行。 例如，您可以將同一資料行轉換成大寫和小寫，並將結果放入兩個不同的資料行。  
  
 在某些情況下，對應可能會造成資料遭到截斷。 例如，當單一位元組字元對應到使用多位元組表示法的字元時，即可能發生截斷。 「字元對應」轉換包含錯誤輸出，可用來將截斷的資料導向不同的輸出。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../../integration-services/data-flow/error-handling-in-data.md)。  
  
 這個轉換有一個輸入、一個輸出與一個錯誤輸出。  
  
## <a name="mapping-operations"></a>對應作業  
 下表描述「字元對應」轉換支援的對應作業。  
  
|作業|描述|  
|---------------|-----------------|  
|位元組反轉|反轉位元組的順序。|  
|全形|將半形字元對應到全形字元。|  
|半形|將全形字元對應到半形字元。|  
|平假名|將片假名字元對應到平假名字元。|  
|片假名|將平假名字元對應到片假名字元。|  
|語言大小寫|套用語言大小寫取代系統規則。 語言大小寫是指 Win32 API 針對突厥語系與其他地區設定所提供的 Unicode 簡易大小寫對應功能。|  
|小寫|將字元轉換成小寫。|  
|簡體中文|將繁體中文字元對應到簡體中文字元。|  
|繁體中文|將簡體中文字元對應到繁體中文字元。|  
|大寫|將字元轉換成大寫。|  
  
## <a name="mutually-exclusive-mapping-operations"></a>互斥對應作業  
 轉換中可執行一項以上的作業。 不過，某些對應作業彼此互斥。 下表列出當您在同一資料行上使用多項作業時適用的限制。 作業 A 和作業 B 資料行中的作業為互斥。  
  
|作業 A|作業 B|  
|-----------------|-----------------|  
|小寫|大寫|  
|平假名|片假名|  
|半形|全形|  
|繁體中文|簡體中文|  
|小寫|平假名、片假名、半形、全形|  
|大寫|平假名、片假名、半形、全形|  
  
## <a name="configuration-of-the-character-map-transformation"></a>字元對應轉換的組態  
 您可以利用下列方式設定「字元對應」轉換：  
  
-   指定要轉換的資料行。  
  
-   指定套用至各資料行的作業。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>字元對應表轉換編輯器
  使用 [字元對應表轉換編輯器]  對話方塊，來選取要套用至資料行資料的字串函數，以及指定對應是就地變更或加入為新資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 使用此對話方塊來選取要使用字串函數轉換的資料行。 您的選擇會在下面的資料表中出現。  
  
 **輸入資料行**  
 從上述資料表檢視選取的輸入資料行。 您也可以藉由使用可用的輸入資料行之清單來變更或移除選擇。  
  
 **目的地**  
 指定字串作業之結果的儲存方式為就地儲存、使用現有的資料行儲存，或將修改的資料儲存為新的資料行。  
  
|值|描述|  
|-----------|-----------------|  
|新增資料行|將資料儲存在新的資料行中。 在 **[輸出別名]** 之下指派資料行名稱。|  
|就地變更|將修改的資料儲存在現有的資料行中。|  
  
 **運算**  
 從字串函數要套用至資料行資料的清單中選取。  
  
|值|描述|  
|-----------|-----------------|  
|小寫|轉換為小寫。|  
|大寫|轉換為大寫。|  
|位元組反轉|藉由反轉位元組的順序來進行轉換。|  
|平假名|將日文片假名字元轉換為平假名。|  
|片假名|將日文平假名字元轉換為片假名。|  
|半形|將全形字元轉換為半形。|  
|全形|將半形字元轉換為全形。|  
|語言大小寫|套用大小寫的語言規則 (突厥語系和其他地區設定的 Unicode 簡單大小寫對應) 來取代系統規則。|  
|簡體中文|將繁體中文字元轉換為簡體中文。|  
|繁體中文|將簡體中文字元轉換為繁體中文。|  
  
 **輸出別名**  
 輸入每一個輸出資料行的別名。 預設為輸入資料行的名稱，後面接著 **[的副本]** ；但是您也可以選擇任何唯一的描述性名稱。  
  
 **設定錯誤輸出**  
 使用 [設定錯誤輸出](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 對話方塊，即可指定此轉換的錯誤處理選項。  
  
  
