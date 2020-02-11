---
title: ADO NET 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6126a352377e988c08a11211d12bb8bc77e93f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153975"
---
# <a name="ado-net-destination"></a>ADO NET 目的地
  ADO NET 目的地會將資料載入使用資料庫資料表或檢視的各種 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]相容資料庫中。 您可以選擇將這些資料載入現有的資料表或檢視中，也可以建立新的資料表並將資料載入新的資料表內。  
  
 您可以使用 ADO NET 目的地來連接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 不過，不支援使用 OLE DB 連接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的詳細資訊，請參閱[一般指導方針與限制 (Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO NET 目的地疑難排解  
 您可以記錄 ADO NET 目的地對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，針對 ADO NET 目的地所執行之將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 ADO NET 目的地對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]**** 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ado-net-destination"></a>設定 ADO NET 目的地  
 此目的地使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員以連接到資料來源，且連接管理員會指定要使用的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者。 如需詳細資訊，請參閱 [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不需要將輸入資料行對應至所有的目的地資料行。 但是，某些目的地資料行的屬性可能需要對應輸入資料行。 否則，可能會發生錯誤。 例如，如果目的地資料行不允許 Null 值，您必須將輸入資料行對應到該目的地資料行。 此外，對應之資料行的資料類型必須相容。 例如，如果 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者不支援，您就無法將具有字串資料類型的輸入資料行對應至具有數值資料類型的目的地資料行。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援將文字插入資料類型設定為影像的資料行內。 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型的詳細資訊，請參閱[&#40;Transact-sql&#41;的資料類型](/sql/t-sql/data-types/data-types-transact-sql)。  
  
> [!NOTE]  
>  ADO NET 目的地不支援將類型設定為 DT_DBTIME 的輸入資料行對應至類型設定為日期時間的資料庫資料行。 如需[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]資料類型的詳細資訊，請參閱[Integration Services 資料類型](integration-services-data-types.md)。  
  
 ADO NET 目的地具有一個規則輸入和一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可以在 [ADO NET 目的地編輯器]**** 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [ADO NET 目的地編輯器 &#40;連線管理員頁面&#41;](../ado-net-destination-editor-connection-manager-page.md)  
  
-   [ADO NET 目的地編輯器 &#40;對應] 頁面&#41;](../ado-net-destination-editor-mappings-page.md)  
  
-   [ADO NET 目的地編輯器 &#40;錯誤輸出頁面&#41;](../ado-net-destination-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [ADO NET 自訂屬性](ado-net-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
  
