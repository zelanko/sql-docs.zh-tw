---
title: Integration Services 交易 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aa40898a63a4d84f9efeaf2c1bf404ab17cea20c
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51642065"
---
# <a name="integration-services-transactions"></a>Integration Services 交易
  封裝使用交易將工作執行的資料庫動作繫結至原子單位，這樣可以保持資料的完整性。 所有 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器類型 (封裝、For 迴圈、Foreach 迴圈和時序容器，以及封裝每個工作的工作主機) 皆可設定成使用交易。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供三個設定交易的選項，分別是 **NotSupported**、 **Supported**及 **Required**。  
  
-   **Required** 指出容器會啟動交易，除非其父容器已經將其啟動。 如果交易已經存在，則容器會聯結交易。 例如，如果未設定為支援交易的封裝包括使用 **Required** 選項的「時序」容器，則「時序」容器會啟動其自己的交易。 如果封裝設定為使用 **Required** 選項，則「時序」容器會聯結封裝交易。  
  
-   **Supported** 指出容器不啟動交易，但會聯結其父容器啟動的任何交易。 例如，如果具有四個「執行 SQL」工作的封裝啟動交易，且全部四個工作都使用 **Supported** 選項，則任何工作失敗時，都會回復「執行 SQL」工作執行的資料庫更新。 如果封裝未啟動交易，則四個「執行 SQL」工作不會由交易繫結，且只會回復由失敗之工作執行的資料庫更新。  
  
-   **NotSupported** 指出容器不啟動交易或聯結現有的交易。 父容器啟動的交易不會影響已設定為不支援交易的子容器。 例如，如果封裝設定為啟動交易，且封裝中的「For 迴圈」容器使用 **NotSupported** 選項，則「For 迴圈」中的工作一旦失敗將無法回復。  
  
 您可以設定容器上的 TransactionOption 屬性來設定交易。 使用 **中的** [屬性] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]視窗，可以設定此屬性，也可以程式設計方式設定屬性。  
  
> [!NOTE]  
>  **TransactionOption** 屬性會影響是否會套用容器所要求的 **IsolationLevel** 屬性值。 如需詳細資訊，請參閱＜ **設定封裝屬性** ＞主題中的 [IsolationLevel](../integration-services/set-package-properties.md)屬性描述。  
  
## <a name="configure-a-package-to-use-transactions"></a>設定封裝來使用交易
將封裝設定成使用交易時，您有兩個選項：  
  
-   擁有封裝的單一交易。 在此情況下，封裝本身會 *「起始」* (Initiate) 這筆交易，而封裝中的個別工作和容器會參與這個單一交易。  
  
-   在封裝中擁有多個交易。 在此情況下，雖然封裝支援交易，但是封裝中的個別工作和容器實際上會起始交易。  
  
 下列程序將描述如何設定這兩個選項。  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>將套件設定成使用單一交易  
 在這個選項中，封裝本身會起始單一交易。 您可以將封裝的 TransactionOption 屬性設定為 **Required**，藉以將此封裝設定成起始這筆交易。  
  
 接著，您可以在這個單一交易中編列特定工作和容器。 若要在交易中編列工作或容器，您可以將該工作或容器的 TransactionOption 屬性設定為 **Supported**。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含您要設定以使用交易之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  以滑鼠右鍵按一下控制流程設計介面背景的任何位置，然後按一下 [屬性]。  
  
5.  在 [屬性] 視窗中，將 TransactionOption 屬性設定為 **Required**。  
  
6.  在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下您要在交易中註冊的工作或容器，然後按一下 [屬性]。  
  
7.  在 [屬性] 視窗中，將 TransactionOption 屬性設定為 **Supported**。  
  
    > [!NOTE]  
    >  若要在交易中編列連接，請註冊在交易中使用連接的工作。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
8.  針對您想要在此交易中註冊的每個工作和容器，重複步驟 6 和 7。  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>將套件設定成使用多個交易  
 在這個選項中，雖然封裝本身支援交易，但是不會啟動交易。 您可以將封裝的 TransactionOption 屬性設定為 **Supported**，藉以將此封裝設定成支援交易。  
  
 接著，您可以將封裝內部的所需工作和容器設定成起始或參與交易。 若要將工作或容器設定成起始交易，您可以將該工作或容器的 TransactionOption 屬性設定為 **Required**。   
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含您要設定成使用交易之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  以滑鼠右鍵按一下控制流程設計介面背景的任何位置，然後按一下 [屬性]。  
  
5.  在 [屬性] 視窗中，將 TransactionOption 屬性設定為 **Supported**。  
  
    > [!NOTE]  
    >  封裝支援交易，但交易是由封裝中的工作或容器所啟動。  
  
6.  在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下要啟動其交易之封裝內的工作或容器，然後按一下 [屬性]。  
  
7.  在 [屬性] 視窗中，將 TransactionOption 屬性設定為 **Required**。  
  
8.  如果交易由容器啟動，請以滑鼠右鍵按一下您要在交易中註冊的工作或容器，然後按一下 [屬性]。  
  
9. 在 [屬性] 視窗中，將 TransactionOption 屬性設定為 **Supported**。  
  
    > [!NOTE]  
    >  若要在交易中編列連接，請註冊在交易中使用連接的工作。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
10. 針對啟動交易的每個工作和容器，重複步驟 6 至 9。  

## <a name="multiple-transactions-in-a-package"></a>套件中有多個交易
在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝中，封裝可以包含不相關的交易。 任何時候如果巢狀容器階層中間的容器不支援交易，而階層中其上面或下面的容器設定為支援交易，則這些容器就會啟動分別的交易。 交易會從巢狀容器階層中最內層的工作到封裝依序進行認可或回復。 不過，內部交易認可後，如果外部交易已中止，則不會回復該交易。  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>套件中有多個交易的範例 
 例如，封裝具有的「時序」容器包含兩個「Foreach 迴圈」容器，而每個容器包含兩個「執行 SQL」工作。 時序容器支援交易，Foreach 迴圈容器不支援，而執行 SQL 工作則支援。 在此範例中，每一個執行 SQL 工作都會啟動自己的交易，而即使時序工作上的交易中止，也不會回復。  
  
 「時序」容器、「Foreach 迴圈」容器和「執行 SQL」工作的 TransactionOption 屬性設定如下：  
  
-   「時序」容器的 TransactionOption 屬性會設為 **Required**。  
  
-   「Foreach 迴圈」容器的 TransactionOption 屬性會設為 **NotSupported**。  
  
-   「執行 SQL」工作的 TransactionOption 屬性會設為 **Required**。  
  
 下圖顯示封裝中五個不相關的交易。 一個交易是由「時序」容器啟動的，四個交易是由「執行 SQL」工作啟動的。  
  
 ![多個交易的實作](../integration-services/media/mw-dts-trans2.gif "多個交易的實作")  
 
## <a name="inherited-transactions"></a>繼承的交易
 封裝可使用「執行封裝」工作執行另一個封裝。 子封裝 (亦即「執行封裝」工作所執行的封裝) 可建立其自己的封裝交易，也可以繼承父封裝交易。  
  
 如果下列兩個情況均成立，則子封裝將會繼承父封裝交易：  
  
-   由一「執行封裝」工作叫用 (Invoke) 該封裝。  
  
-   叫用該封裝的「執行封裝」工作亦聯結父封裝交易。  
  
 除非子封裝自行聯結交易，否則子封裝中的容器和工作無法聯結父封裝交易。  
  
### <a name="example-of-inherited-transactions"></a>繼承的交易範例  
 在下圖中，有三個使用交易的封裝。 每一個封裝都包含多個工作。 為強調交易的行為，只會顯示「執行封裝」工作。 封裝 A 執行封裝 B 和 C。而封裝 B 又執行封裝 D 和 E，封裝 C 執行封裝 F。  
  
 封裝和工作具有下列交易屬性：  
  
-   在封裝 A 和 C 上，**TransactionOption** 設為 **Required**   
  
-   在封裝 B 和 D 上，以及在「執行封裝 B」、「執行封裝 D」和「執行封裝 F」工作上，**TransactionOption** 設為 **Supported** 。  
  
-   在封裝 E 上，以及在「執行封裝 C」和「執行封裝 E」工作上，**TransactionOption** 設為 **NotSupported** 。  
  
 ![繼承的交易流程](../integration-services/media/mw-dts-executepack.gif "繼承的交易流程")  
  
 只有封裝 B、D 和 F 可從其父封裝繼承交易。  
  
 封裝 B 和 D 會繼承由封裝 A 啟動的交易。  
  
 封裝 F 會繼承由封裝 C 啟動的交易。  
  
 封裝 A 和 C 會控制其自己的交易。  
  
 封裝 E 不使用交易。  
 
  
## <a name="external-resources"></a>外部資源  
  
-   位於 www.mssqltips.com 的部落格項目： [如何在 SQL Server Integration Services SSIS 中使用交易](https://go.microsoft.com/fwlink/?LinkId=157783)  
  
## <a name="see-also"></a>另請參閱  
 [繼承的交易](https://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [多個交易](https://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  
