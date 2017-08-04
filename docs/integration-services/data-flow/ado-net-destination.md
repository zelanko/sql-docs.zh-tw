---
title: "ADO NET 目的地 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetdest.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 19dc271dee6898d253f51be7c49efe7f0aaa5e7a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="ado-net-destination"></a>ADO NET 目的地
  ADO NET 目的地會將資料載入使用資料庫資料表或檢視的各種 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]相容資料庫中。 您可以選擇將這些資料載入現有的資料表或檢視中，也可以建立新的資料表並將資料載入新的資料表內。  
  
 您可使用 ADO NET 目的地，連接至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 不過，不支援使用 OLE DB 連接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的詳細資訊，請參閱 [Azure SQL Database 一般限制與方針](http://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO NET 目的地疑難排解  
 您可以記錄 ADO NET 目的地對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，針對 ADO NET 目的地所執行之將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 ADO NET 目的地對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱[封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ado-net-destination"></a>設定 ADO NET 目的地  
 此目的地使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員以連接到資料來源，且連接管理員會指定要使用的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者。 如需詳細資訊，請參閱 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不需要將輸入資料行對應至所有的目的地資料行。 但是，某些目的地資料行的屬性可能需要對應輸入資料行。 否則，可能會發生錯誤。 例如，如果目的地資料行不允許 Null 值，您必須將輸入資料行對應到該目的地資料行。 此外，對應之資料行的資料類型必須相容。 例如，如果 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者不支援，您就無法將具有字串資料類型的輸入資料行對應至具有數值資料類型的目的地資料行。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支援將文字插入到資料行的資料型別設定為影像。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的詳細資訊，請參閱 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)＞。  
  
> [!NOTE]  
>  ADO NET 目的地不支援將類型設定為 DT_DBTIME 的輸入資料行對應至類型設定為日期時間的資料庫資料行。 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 ADO NET 目的地具有一個規則輸入和一個錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可以在 [ADO NET 目的地編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [ADO NET 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/ado-net-destination-editor-connection-manager-page.md)  
  
-   [ADO NET 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)  
  
-   [ADO NET 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO NET 自訂屬性](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
  
