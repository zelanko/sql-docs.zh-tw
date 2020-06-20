---
title: 工作6：設定同義字 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a6f4e870dca91e952fbeea95ef8f1198c64d8d6b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054275"
---
# <a name="task-6-setting-synonyms"></a>工作 6：設定同義字
  在這項工作中，您會將**Country**網域的兩個定義域值（**美國**和**美國**）設定為以**美國**做為前置值的同義字。 因為在建立**國家/地區**網域時選取了 [**使用前置值**] 選項，所以**country**網域的任何**美國**值都會輸出為**美國**（美國是前置值）。 如需詳細資訊，請參閱[變更定義域值](https://msdn.microsoft.com/library/hh510408.aspx)。

1.  從網域清單中選取 [**國家/地區**]。

2.  切換至 [**定義域值**] 索引標籤。

3.  按一下工具列上的 [**加入新的定義域值**] 按鈕。

4.  輸入**USA**作為值，然後按**enter**。

5.  使用 CTRL 或 SHIFT**鍵，以**滑鼠右鍵按一下選取的專案 **，然後按一下**[**設為同義字**]。 DQS 會將這些值分組在一起，並將其中一個值指定為將用來取代其他值的前置值。

     ![[設為同義字] 功能表](../../2014/tutorials/media/et-settingsynonyms-01.jpg "[設為同義字] 功能表")

6.  請注意，**美國**已設定為前置值。 如果您想要讓 USA 成為前置值，可以用滑鼠右鍵按一下 [美國]，然後選取 [**設定為前置**選項]。 在本教學課程中，我們會使用**美國**做為前置值。

     ![United States 和 USA 為同義字](../../2014/tutorials/media/et-settingsynonyms-02.jpg "United States 和 USA 為同義字")

## <a name="next-step"></a>後續步驟
 [工作 7：建立複合定義域](../../2014/tutorials/task-7-creating-a-composite-domain.md)


