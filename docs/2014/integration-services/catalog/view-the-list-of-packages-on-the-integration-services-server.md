---
title: 檢視 Integration Services 伺服器上的套件清單 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 67a992d1-7524-4f4b-b3d8-ebd9e5ea82a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96d752b84506ea3e9275e5f16903c19288c6ff92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62836211"
---
# <a name="view-the-list-of-packages-on-the-integration-services-server"></a>檢視 Integration Services 伺服器上的封裝清單
  您可以使用下列兩種方式之一，檢視儲存在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的封裝清單。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 若要檢視儲存在伺服器上的封裝清單，請查詢 [catalog.packages &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database) 檢視。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中  
 若要使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的物件總管檢視儲存在伺服器上的封裝，請依照以下的程序進行。  
  
### <a name="to-view-packages-using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>若要使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。 亦即連接到主控 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 資料庫的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[Integration Services 目錄]** 節點以顯示 **[SSISDB]** 節點。  
  
4.  展開 **[SSISDB]** 節點以顯示一個或多個資料夾的清單。 每個資料夾在 **[專案]** 資料夾中都包含一個或多個專案，而且每個專案都在 **[封裝]** 資料夾中包含一個或多個封裝。  
  
  
