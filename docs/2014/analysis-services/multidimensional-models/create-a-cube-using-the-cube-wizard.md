---
title: 使用 Cube 精靈建立 Cube |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], creating
ms.assetid: d46d659c-3a4e-4364-94ac-f5eb6ba0ec25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ffd5880120184249d89c4d702b30c8d6e01e1f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076496"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>使用 Cube 精靈來建立 Cube
  您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 [Cube 精靈] 來建立新的 Cube。  
  
### <a name="to-create-a-new-cube"></a>建立新的 Cube  
  
1.  在方案總管  中，以滑鼠右鍵按一下 [Cube]  ，然後按一下 [新增 Cube]  。  
  
2.  在 [Cube 精靈] 的 [選取建立方法]  頁面上，選取 [使用現有的資料表]  ，然後按一下 [下一步]  。  
  
    > [!NOTE]  
    >  您可能偶爾必須在不使用現有資料表的情況下建立 Cube。 若要建立空白的 Cube，請選取 [建立空白 Cube]  。 若要產生資料表，請選取 [在資料來源中建立資料表]  。  
  
3.  在 [選取量值群組資料表]  頁面上，執行下列程序：  
  
    1.  在 [資料來源檢視]  清單中，選取資料來源檢視。  
  
    2.  在 [量值群組資料表]  清單中，選取將用來建立量值群組的資料表。  
  
    3.  按一下 [下一步]  。  
  
4.  在 [選取量值]  頁面上，選取您要包含在 Cube 中的量值，然後按一下 [下一步]  。  
  
     (選擇性) 您可以變更量值和量值群組的名稱。  
  
5.  在 [選取現有維度]  頁面上，選取您要包含在 Cube 中的現有維度，然後按一下 [下一步]  。  
  
    > [!NOTE]  
    >  如果維度已經存在任何選取量值群組的資料庫中，就會顯示 [選取現有維度]  頁面。  
  
6.  在 [選取新維度]  頁面上，選取要建立的新維度，然後按一下 [下一步]  。  
  
    > [!NOTE]  
    >  如果有任何資料表適合當作維度資料表，而且這些資料表尚未由現有的維度使用，就會顯示 [選取新維度]  頁面。  
  
7.  在 [選取遺漏維度索引鍵]  頁面上，選取維度的索引鍵，然後按一下 [下一步]  。  
  
    > [!NOTE]  
    >  如果您指定的任何維度資料表沒有定義索引鍵，就會顯示 [選取遺漏維度索引鍵]  頁面。  
  
8.  在 [正在完成精靈]  頁面上，輸入新 Cube 的名稱，然後檢閱 Cube 的結構。 如果您要進行任何變更，按一下 [上一步]  ，否則，按一下 [完成]  。  
  
    > [!NOTE]  
    >  在您完成「Cube 精靈」之後，可以使用「Cube 設計師」來設定 Cube。 此外，您也可以使用「維度設計師」，在您建立的維度中加入、移除和設定屬性與階層。  
  
  
