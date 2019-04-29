---
title: SQL Server Compact Edition 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c59157c8d6beccdbb2d3e853cb6e035f9f89f61c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901074"
---
# <a name="sql-server-compact-edition-destination"></a>SQL Server Compact Edition 目的地
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地會將資料寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫。  
  
> [!NOTE]  
>  在 64 位元電腦上，您必須以 32 位元模式執行連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料來源的封裝。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 資料來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 提供者只有提供 32 位元版本。  
  
 您可以透過指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地將資料插入所在的資料表名稱來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地的 TableName 自訂屬性包含資料表名稱。  
  
 此目的地會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員連接到資料來源，且連線管理員會指定要使用的 OLE DB 提供者。 如需詳細資訊，請參閱 [SQL Server Compact Edition 連線管理員](../connection-manager/sql-server-compact-edition-connection-manager.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地包括 TableName 自訂屬性；屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../expressions/use-property-expressions-in-packages.md)和 [SQL Server Compact Edition 目的地自訂屬性](sql-server-compact-edition-destination-custom-properties.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 目的地具有一個輸入，且不支援錯誤輸出。  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>設定 SQL Server Compact Edition 目的地  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [SQL Server 目的地自訂屬性](sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](data-flow.md)  
  
  
