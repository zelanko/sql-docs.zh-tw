---
title: 將封裝設定成使用交易 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcbe13bd63284cdeeba219eb0a0cbcdc4084d4b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835212"
---
# <a name="configure-a-package-to-use-transactions"></a>設定封裝來使用交易
  將封裝設定成使用交易時，您有兩個選項：  
  
-   擁有封裝的單一交易。 在此情況下，封裝本身會 *「起始」* (Initiate) 這筆交易，而封裝中的個別工作和容器會參與這個單一交易。  
  
-   在封裝中擁有多個交易。 在此情況下，雖然封裝支援交易，但是封裝中的個別工作和容器實際上會起始交易。  
  
 下列程序將描述如何設定這兩個選項。  
  
## <a name="configuring-a-single-transaction"></a>設定單一交易  
 在這個選項中，封裝本身會起始單一交易。 您將封裝設定成起始這筆交易之封裝的 TransactionOption 屬性設定`Required`。  
  
 接著，您可以在這個單一交易中編列特定工作和容器。 若要編列工作或容器，在交易中的，您可以設定該工作或容器的 TransactionOption 屬性`Supported`。  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>將封裝設定成使用單一交易  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含您要設定以使用交易之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  以滑鼠右鍵按一下控制流程設計介面背景的任何位置，然後按一下 [屬性]。  
  
5.  在 [**屬性**] 視窗中，將 TransactionOption 屬性設定為`Required`。  
  
6.  在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下您要在交易中註冊的工作或容器，然後按一下 [屬性]。  
  
7.  在 [**屬性**] 視窗中，將 TransactionOption 屬性設定為`Supported`。  
  
    > [!NOTE]  
    >  若要在交易中編列連接，請註冊在交易中使用連接的工作。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](connection-manager/integration-services-ssis-connections.md)。  
  
8.  針對您想要在此交易中註冊的每個工作和容器，重複步驟 6 和 7。  
  
## <a name="configuring-multiple-transactions"></a>設定多個交易  
 在這個選項中，雖然封裝本身支援交易，但是不會啟動交易。 您將套件設定為支援交易之封裝的 TransactionOption 屬性設定`Supported`。  
  
 接著，您可以將封裝內部的所需工作和容器設定成起始或參與交易。 若要設定工作或容器，以起始交易，您可以設定該工作或容器的 TransactionOption 屬性`Required`。  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>將封裝設定成使用多個交易  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含您要設定成使用交易之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  以滑鼠右鍵按一下控制流程設計介面背景的任何位置，然後按一下 [屬性]。  
  
5.  在 [**屬性**] 視窗中，將 TransactionOption 屬性設定為`Supported`。  
  
    > [!NOTE]  
    >  封裝支援交易，但交易是由封裝中的工作或容器所啟動。  
  
6.  在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下要啟動其交易之封裝內的工作或容器，然後按一下 [屬性]。  
  
7.  在 [**屬性**] 視窗中，將 TransactionOption 屬性設定為`Required`。  
  
8.  如果交易由容器啟動，請以滑鼠右鍵按一下您要在交易中註冊的工作或容器，然後按一下 [屬性]。  
  
9. 在 [**屬性**] 視窗中，將 TransactionOption 屬性設定為`Supported`。  
  
    > [!NOTE]  
    >  若要在交易中編列連接，請註冊在交易中使用連接的工作。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](connection-manager/integration-services-ssis-connections.md)。  
  
10. 針對啟動交易的每個工作和容器，重複步驟 6 至 9。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 交易](integration-services-transactions.md)  
  
  
