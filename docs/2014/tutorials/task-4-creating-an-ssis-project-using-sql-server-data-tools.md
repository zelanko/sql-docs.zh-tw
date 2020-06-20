---
title: 工作4：使用 SQL Server Data Tools 建立 SSIS 專案 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 935409eeb7724f4c9807aecc8ec69c4cba0735a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006502"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>工作 4：使用 SQL Server Data Tools 建立 SSIS 專案
  在這項工作中，您會使用**SQL Server Data Tools**來建立 SSIS 專案，以自動化清理和比對供應商資料。

1.  啟動 **SQL Server Data Tools**。 按一下 [開始]，指向 [**所有程式**]，展開 [ **Microsoft SQL Server 2012**]，然後按一下 [ **SQL Server Data Tools**]。

2.  在 [ **檔案** ] 功能表中，指向 [ **新增**]，然後按一下 [ **專案**]。

3.  展開 [**已安裝的範本**] 窗格中的 [**商業智慧**]，然後選取 [ **Integration Services**]。

     ![Visual Studio - [新增專案] 對話方塊](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio - [新增專案] 對話方塊")

4.  在**專案類型清單**中，選取 [ **Integration Services 專案**]。

5.  針對 [**名稱**] 輸入**CleanseAndCurateSuppliers** ，然後按一下 **[確定]**。

6.  在**方案總管**] 視窗中，以滑鼠右鍵按一下 **.dtsx** ，然後選取 [**重新命名**]。 如果您沒有看到 [**方案總管**] 視窗，請按一下功能表列上的 [**查看**]，然後按一下 [**方案總管**]。

     ![Package.dtsx - [重新命名] 功能表](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx - [重新命名] 功能表")

7.  輸入**cleanseandcurate.cleanse supplier data.guid. .dtsx** ，然後按**enter**。 請確定**擴充**功能保持不變 **。 .dtsx**。

## <a name="next-step"></a>後續步驟
 [工作 5：新增資料流程工作](task-5-adding-data-flow-task.md)


