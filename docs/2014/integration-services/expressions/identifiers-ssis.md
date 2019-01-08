---
title: 識別碼 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 83c0d4b810f3835659849bd63766d45b101d5339
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360270"
---
# <a name="identifiers-ssis"></a>識別碼 (SSIS)
  在運算式中，識別碼是可供運算的資料行和變數。 運算式可使用一般和限定識別碼。  
  
## <a name="regular-identifiers"></a>一般識別碼  
 一般識別碼是不需要額外限定詞的識別碼。 例如， **AdventureWorks**資料庫的 **Contacts** 資料表中的 **MiddleName** 資料行即為一般識別碼。  
  
 一般識別碼的命名必須按照下列規則：  
  
-   名稱的第一個字元必須是 Unicode Standard 2.0 所定義的字母，或者底線 (_)。  
  
-   後續的字元可以是 Unicode Standard 2.0 所定義的字母或數字、底線 (_)、\@、$ 及 # 字元。  
  
> [!IMPORTANT]  
>  除了列出的字元之外，內嵌的空格和特殊字元在一般識別碼中無效。 若要使用空格和特殊字元，您必須使用限定識別碼，而非一般識別碼。  
  
## <a name="qualified-identifiers"></a>限定識別碼  
 限定識別碼是以方括號分隔的識別碼。 識別碼可能需要分隔符號，因為識別碼的名稱包含空白，或是因為識別碼名稱的開頭不是字母或底線字元。 例如， **Middle Name** 資料行名稱必須以方括號限定，並於運算式中撰寫為 [Middle Name]。  
  
 如果識別碼的名稱包含空白，或如果名稱不是有效的一般識別碼名稱，則該識別碼必須加以限定。 運算式評估工具會使用左、右方括號 ([]) 限定識別碼。 方括號會放在字串的第一個和最後一個位置。 例如，識別碼 5$> 會變成 [5$>]。 方括號可用於資料行名稱、變數名稱，以及函數名稱。  
  
 如果您使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師對話方塊建立運算式，則一般識別碼會自動加上方括號。 不過，只有在名稱包含無效字元時才需要方括號。 例如，名為 **MiddleName** 的資料行是有效的資料行，不需要方括號。  
  
 您無法參考運算式中包含方括號的資料行名稱。 例如，資料行名稱 **Column[1]** 不可用於運算式中。 若要在運算式中使用資料行，則必須將它重新命名為不含方括號的名稱。  
  
## <a name="lineage-identifiers"></a>歷程識別碼  
 運算式可以使用歷程識別碼來參考資料行。 當您初次建立封裝時，會自動指派歷程識別碼。 您可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，於 [進階編輯器] 對話方塊的 [資料行屬性] 索引標籤上檢視資料行的歷程識別碼。  
  
 如果您使用資料行本身的歷程識別碼參考該資料行，則識別碼前面必須包含井字號 (#) 字元。 例如，歷程識別碼 147 的資料行必須以 #147 的形式參考。  
  
 如果運算式剖析成功，則運算式評估工具會以對話方塊中的資料行名稱取代歷程識別碼。  
  
## <a name="unique-column-names"></a>唯一資料行名稱  
 封裝中使用的多個元件可公開同名的資料行。 如果這些資料行是在運算式中使用，則須使其意義明確，運算式才能成功剖析。 運算式評估工具支援用來識別資料行來源的虛線標記法。 例如，兩個名為 **Age** 的資料行會變成 **FlatFileSource.Age** 和 **OLEDBSource.Age**，這表示其來源為 FlatFileSource 或 OLEDBSource。 剖析器會將完整名稱視為單一資料行名稱。  
  
 來源元件名稱和資料行名稱會分別加以限定。 下列範例說明，在虛線標記法中方括號的有效用法：  
  
-   來源元件名稱包含空白。  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   資料行名稱的第一個字元無效。  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   來源元件和資料行名稱含有無效字元。  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  如果虛線標記法中的兩個元素都加上一對方括號，則運算式評估工具會將這對元素解譯為單一識別碼，而非來源資料行組合。  
  
## <a name="variables-in-expressions"></a>運算式中的變數  
 在運算式中參考變數時，必須包括 \@ 前置詞。 例如，**Counter** 變數是使用 \@Counter 來參考。 \@ 字元並非變數名稱的一部分；該字元僅供運算式評估工具用來識別變數。 如果您使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具提供的對話方塊建置運算式，則 \@ 字元會自動加入變數名稱中。 在 \@ 字元和變數名稱之間加入空白是無效的格式。  
  
 變數名稱與其他一般識別碼的名稱遵循相同的規則：  
  
-   名稱的第一個字元必須是 Unicode Standard 2.0 所定義的字母，或者底線 (_)。  
  
-   後續的字元可以是 Unicode Standard 2.0 所定義的字母或數字、底線 (_)、\@、$ 及 # 字元。  
  
 如果變數名稱包含所列出字元以外的字元，則變數必須加上方括號。 例如，含空白的變數名稱必須加上方括號。 左方括弧會接在 \@ 字元後面。 例如，**My Name** 變數會以 \@[My Name] 的形式參考。 不可在變數名稱和方括號之間加入空白。  
  
> [!NOTE]  
>  使用者定義變數和系統變數的名稱會區分大小寫。  
  
## <a name="unique-variable-names"></a>唯一變數名稱  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援自訂變數並提供一組系統變數。 自訂變數預設屬於 **使用者** 命名空間，而系統變數則屬於 **系統** 命名空間。 您可以為自訂變數建立額外的命名空間，並更新命名空間的名稱，以符合應用程式的需要。 運算式產生器會列出所有命名空間中適用的變數。  
  
 所有變數都有範圍且屬於命名空間。 變數擁有封裝範圍，或封裝中容器或工作的範圍。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的運算式產生器只會列出範圍內的變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。  
  
 運算式中使用的變數必須有唯一名稱，運算式評估工具才能正確評估運算式。 如果封裝使用多個同名的變數，則其命名空間必須有所區別。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供由兩個冒號 (::) 組成的命名空間解析運算子，可用於指出變數所屬的命名空間。 例如，下列運算式使用兩個名稱為 **Count**的變數；其中一個屬於 **使用者** 命名空間，另一個屬於 **MyNamespace** 命名空間。  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  您必須將命名空間和限定變數名稱的組合加上方括號，運算式評估工具才能辨認該變數。  
  
 如果值**計數**中**使用者**命名空間為 10，而值**計數**中**MyNamespace**為 2，運算式評估為`true`因為運算式評估工具可以辨認這兩個不同的變數。  
  
 即使變數名稱不是唯一的，也不會發生錯誤。 但運算式評估工具只會使用一個變數執行個體評估運算式，並傳回不正確的結果。 例如，下列運算式要用來比較兩個不同的值 （10 和 2）**計數**變數，但運算式會評估為`false`因為運算式評估工具會使用相同的執行個體的**計數**變數兩次。  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>相關內容  
 pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](https://go.microsoft.com/fwlink/?LinkId=217683)  
  
  
