---
title: Integration Services 交易 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0359ca10e7279f4a80bec082a8e049f4641c9b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767627"
---
# <a name="integration-services-transactions"></a>Integration Services 交易
  封裝使用交易將工作執行的資料庫動作繫結至原子單位，這樣可以保持資料的完整性。 所有 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器類型 (封裝、For 迴圈、Foreach 迴圈和時序容器，以及封裝每個工作的工作主機) 皆可設定成使用交易。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了三種設定交易的選項：**NotSupported**、**Supported** 和 **Required**。  
  
-   **Required** 指出容器會啟動交易，除非其父容器已經將其啟動。 如果交易已經存在，則容器會聯結交易。 例如，如果未設定為支援交易的封裝包括使用 **Required** 選項的「時序」容器，則「時序」容器會啟動其自己的交易。 如果封裝設定為使用 **Required** 選項，則「時序」容器會聯結封裝交易。  
  
-   **Supported** 指出容器不啟動交易，但會聯結其父容器啟動的任何交易。 例如，如果具有四個「執行 SQL」工作的封裝啟動交易，且全部四個工作都使用 **Supported** 選項，則任何工作失敗時，都會回復「執行 SQL」工作執行的資料庫更新。 如果封裝未啟動交易，則四個「執行 SQL」工作不會由交易繫結，且只會回復由失敗之工作執行的資料庫更新。  
  
-   **NotSupported** 指出容器不啟動交易或聯結現有的交易。 父容器啟動的交易不會影響已設定為不支援交易的子容器。 例如，如果封裝設定為啟動交易，且封裝中的「For 迴圈」容器使用 **NotSupported** 選項，則「For 迴圈」中的工作一旦失敗將無法回復。  
  
 您可以設定容器上的 TransactionOption 屬性來設定交易。 使用 **中的** [屬性] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]視窗，可以設定此屬性，也可以程式設計方式設定屬性。  
  
> [!NOTE]  
>  `TransactionOption` 屬性會影響是否會套用容器所要求的 `IsolationLevel` 屬性值。 如需詳細資訊，請參閱說明`IsolationLevel`主題中的屬性[設定封裝屬性](set-package-properties.md)。  
  
### <a name="to-configure-a-package-to-use-transactions"></a>若要設定封裝使用交易  
  
-   [設定套件來使用交易](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>外部資源  
  
-   位於 www.mssqltips.com 的部落格項目： [如何在 SQL Server Integration Services SSIS 中使用交易](https://go.microsoft.com/fwlink/?LinkId=157783)  
  
## <a name="see-also"></a>另請參閱  
 [繼承的交易](../../2014/integration-services/inherited-transactions.md)   
 [多個交易](../../2014/integration-services/multiple-transactions.md)  
  
  
