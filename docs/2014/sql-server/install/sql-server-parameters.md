---
title: SQL Server 參數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine analysis [Upgrade Advisor]
- SQL Server Upgrade Advisor, Database Engine
- Upgrade Advisor [SQL Server], Database Engine
- analyzing system [Upgrade Advisor], Database Engine
ms.assetid: 44a18bfe-e593-47a5-995f-382c01d3f618
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 96d06ac85b37ef5d91a49381f97f81ee7a2d87e2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011827"
---
# <a name="sql-server-parameters"></a>SQL Server 參數
  在這個頁面上，您可以設定分析器將用於 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 分析的參數。 您可以分析一個、許多個或所有資料庫、分析使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 所建立的追蹤檔案，以及分析 SQL 批次檔。  
  
> [!NOTE]  
>  只有在您提交要分析的追蹤檔案或 SQL 批次檔時，才能偵測出某些升級問題。  
  
## <a name="options"></a>選項  
 **要分析的資料庫**  
 若要分析所有資料庫，請選取 [**所有資料庫**] 核取方塊。 若要分析資料庫的選取範圍，請選取要包括在掃描中之每個資料庫旁的核取方塊。  
  
 **分析追蹤檔案**  
 選取此核取方塊可以在檔案系統中分析追蹤檔案。  
  
 **追蹤檔案的路徑**  
 您可以分析一個或多個檔案。 您可以瀏覽至某個位置並選取多個檔案，也可以提供多個檔案名稱。 請使用每個檔案的完整路徑名稱、加入檔案名稱，然後使用縱線字元 (|) 來分隔項目。  
  
 如果您啟用 [**分析追蹤**檔案]，則會停用 **[下一步]** ，直到您輸入路徑名稱和檔案名為止。  
  
 **分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 批次檔**  
 選取此核取方塊可以在檔案系統中分析 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次檔。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]批次檔的路徑**  
 您可以分析一個或多個批次檔。 您可以瀏覽至某個位置並選取多個檔案，也可以輸入多個檔案名稱。 請使用每個檔案的完整路徑名稱、加入檔案名稱，然後使用縱線字元 (|) 來分隔項目。  
  
 如果您啟用 [**分析 SQL 批次檔**]，[**下一步]** 按鈕會停用，直到您輸入路徑名稱和檔案名為止。  
  
 **SQL 批次分隔符號**  
 用來分隔 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式批次的文字。 預設值為**GO**。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
