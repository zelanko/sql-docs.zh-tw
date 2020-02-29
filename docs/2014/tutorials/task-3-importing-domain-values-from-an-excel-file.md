---
title: 工作3：從 Excel 檔案匯入定義域值 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 36c34be6d994c543eb17f8c923fcf62c0fdd53d4
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177268"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>工作 3：從 Excel 檔案匯入定義域值

  在此工作中，您會從 Excel 檔案的工作表匯入**State**定義域的值。

1.  按一下 [**定義域清單**] 中的 [**狀態**網域]。

2.  確定 [**定義域值**] 索引標籤在右窗格中為作用中。

3.  在右窗格中，從工具列按一下 [匯**入值**] 按鈕旁邊的**向下箭**號，然後按一下 [**從 Excel 匯入有效值**]。

     ![[從 Excel 匯入有效值] 功能表](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "[從 Excel 匯入有效值] 功能表")

4.  按一下 **[流覽]**，選取 [**供應商 .xls**]，然後按一下 [**開啟**]。

5.  針對**工作表**選取 [ **StatesToImport $** ]。

     ![[匯入定義域值] 對話方塊](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "[匯入定義域值] 對話方塊")

6.  按一下 **[確定**] 以關閉 [匯**入定義域值**] 對話方塊。 您應該會看到您已匯入到清單中的所有州別名稱。 請注意，匯入之後會自動選取 [**只顯示新**選項]。 當您匯入值，但沒有看到清單中的舊值時，這是因為在匯入之後會自動啟用此選項。 若要查看所有值，請清除核取方塊。 如果您重新匯入相同的一組值，任何值都不會匯入，因為它們已經存在於定義域中。

     ![只顯示定義域值上的新核取方塊](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "只顯示定義域值上的新核取方塊")

## <a name="next-step"></a>後續步驟
 [工作 4：設定定義域規則](../../2014/tutorials/task-4-setting-domain-rules.md)


