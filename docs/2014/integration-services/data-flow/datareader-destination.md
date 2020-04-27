---
title: DataReader 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 694e85a56686379d089f3c2fc11721e4dd6f8642
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827547"
---
# <a name="datareader-destination"></a>DataReader 目的地
  DataReader 目的地使用 ADO.NET `DataReader` 介面公開資料流程中的資料。 然後，資料可以由其他應用程式取用。 例如，您可以設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表的資料來源，以使用執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件的結果。 若要這樣做，請建立實作 DataReader 目的地的資料流程。  
  
 如需以程式設計方式存取和讀取 DataReader 目的地之值的詳細資訊，請參閱 [載入本機封裝的輸出](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)。  
  
## <a name="configuration-of-the-datareader-destination"></a>設定 DataReader 目的地  
 您可以指定 DataReader 目的地的逾時值，並指示逾時發生時目的地是否失敗。 如果應用程式未在指定時間內要求資料，便會發生逾時。  
  
 DataReader 目的地有一個輸入。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [資料讀取元目的地自訂屬性](datareader-destination-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
  
