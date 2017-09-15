---
title: "參數化命令與中介計算命令 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8821ebd2fb20cf32c6b1921c36e45404421f415b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>參數化的命令與中介計算命令
一般的參數化的圖形附加命令有一個子句，會建立父**資料錄集**查詢命令與另一個子句，以建立子系**資料錄集**使用參數化的查詢命令：也就是包含的參數預留位置的命令 (問號，"？")。 產生的形狀**資料錄集**具有父代所佔高層級的兩個層級和子系會佔用較低層級。  
  
 建立子子句**資料錄集**現在可能任意數目的巢狀圖形計算命令，其中巢狀最深處命令包含參數化的查詢。 產生的形狀**資料錄集**具有父代所佔的最上方的層級的多個層級、 子系所佔的點陣圖最少的層級和任意數目的**資料錄集**所產生的 s圖形計算指令所佔用的中介層級。  
  
 一般使用這項功能是要叫用的彙總函式和群組功能 shapeCOMPUTE 命令建立的中介**資料錄集**物件的子系的分析資訊**資料錄集**. 此外，因為這是參數化的圖形命令時，每次的父代的章節資料行存取時，新的子系**資料錄集**可擷取。 因為的中介層級都衍生自子，它們也會重新計算。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
