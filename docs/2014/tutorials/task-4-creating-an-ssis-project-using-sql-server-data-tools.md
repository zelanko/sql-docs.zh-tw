---
title: 工作 4： 建立使用 SQL Server Data Tools 的 SSIS 專案 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6fb09370b01a88c23d75b843d588626ed96c9b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208068"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>工作 4：使用 SQL Server Data Tools 建立 SSIS 專案
  在這個工作中，您必須建立 SSIS 專案使用**SQL Server Data Tools**自動化清理和比對供應商資料。  
  
1.  啟動 **SQL Server Data Tools**。 按一下 [開始]，指向**所有程式**，展開**Microsoft SQL Server 2012**，然後按一下**SQL Server Data Tools**。  
  
2.  在 [ **檔案** ] 功能表中，指向 [ **新增**]，然後按一下 [ **專案**]。  
  
3.  依序展開**Business Intelligence**中**已安裝的範本**窗格，然後選取**Integration Services**。  
  
     ![Visual Studio-新增專案對話方塊](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio-新增專案對話方塊")  
  
4.  選取  **Integration Services 專案**中**專案類型清單**。  
  
5.  型別**CleanseAndCurateSuppliers** for**名稱**然後按一下**確定**。  
  
6.  在 **方案總管 中** 視窗中，以滑鼠右鍵按一下**Package.dtsx** ，然後選取**重新命名**。 如果您沒有看到**方案總管** 視窗中，按一下**檢視**功能表列，然後按一下 **方案總管 中**。  
  
     ![Package.dtsx-重新命名 功能表](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx-重新命名 功能表")  
  
7.  型別**CleanseAndCurate.dtsx**然後按**ENTER**。 請確定**延伸模組**維持 **.dtsx**。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 5：新增資料流程工作](task-5-adding-data-flow-task.md)  
  
  
