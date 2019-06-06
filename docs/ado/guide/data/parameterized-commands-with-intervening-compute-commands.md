---
title: 參數化命令與中介 COMPUTE 命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b33feb8075babd50f67b6c01da5afadcd1c33e0b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700515"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>參數化命令與中介 COMPUTE 命令
一般的參數化的圖形附加命令有一個子句，會建立父代**資料錄集**查詢命令與建立的子系的另一個子句**資料錄集**使用參數化的查詢命令-也就是將包含的參數預留位置的命令 (問號，"？")。 產生的形狀**資料錄集**有父代會佔用較高層級的兩個層級和子系會佔用低層級。  
  
 建立子子句**資料錄集**現在可能任意數目的巢狀圖形計算命令，其中最深的巢狀的命令包含參數化的查詢。 產生的形狀**資料錄集**有多個層級，父代所佔用的最上方的層級、 點陣圖最少的層級和任意數目的子系會佔用**資料錄集**所產生的 s圖形計算命令佔用的中介層級。  
  
 典型的使用這項功能是要叫用的彙總函式和 shapeCOMPUTE 群組功能的命令建立中介**Recordset**物件的子系的分析資訊**資料錄集**. 此外，因為這是參數化的圖形命令時，每次之父代的章節資料行存取時，新的子系**資料錄集**可能擷取。 因為中介層級都衍生自子系，也是將計算的。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
