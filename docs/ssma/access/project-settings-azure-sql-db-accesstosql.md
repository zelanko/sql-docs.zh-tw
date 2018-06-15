---
title: 專案設定 (Azure SQL DB) (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9d1666bf70cb07e616995dbd8f14fe4522cadc99
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774114"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>專案設定 (Azure SQL DB) (AccessToSQL)
SQL Azure 專案設定可讓您設定 新增連接對話方塊中，而且也允許 活動訊號機制實作 SQL Azure 連接中的 SQL Azure 資料庫尾碼。  
  
SQL Azure 窗格位於**專案設定**和**預設專案設定**對話方塊。  
  
-   使用 [專案設定] 對話方塊，設定目前專案的組態選項。 若要存取 SQL Azure 的設定，在**工具**功能表上，選取**專案設定**，按一下 **一般**底部的左的窗格，然後選取**SQL Azure**。  
  
-   您可以使用預設專案設定 對話方塊來設定所有專案的組態選項。 若要存取 SQL Azure 的設定，在**工具**功能表上，選取**DefaultProject 設定**，在中，選取專案類型為"SQL Azure"**移轉的目標版本**下拉式方塊，以存取設定，在 SQL Azure 窗格中，按一下**一般**底部的左的窗格，然後選取**SQL Azure**。  
  
## <a name="options"></a>選項。  
  
## <a name="connectivity"></a>連接性  
**活動訊號間隔時間**  
  
指定要用於活動訊號機制，以保持存留在 SQL Azure 連接時間間隔 ' 分鐘： 秒數的格式。  
  
**預設值**:' 4:45 '  
  
應該指定的值在我： ss 的格式 (例如，' 4:45 '或' 0:50 ')。  
  
**SQL Azure 伺服器後置詞**  
  
指定的 SQL Azure 伺服器尾碼  
  
**預設值**: '.database.windows.net'。  
  
