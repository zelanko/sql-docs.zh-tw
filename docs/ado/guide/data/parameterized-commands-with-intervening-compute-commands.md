---
title: 使用中間計算命令的參數化命令 |Microsoft Docs
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
ms.openlocfilehash: fb6bc2b9f7e53caf28f44daf39815850940b9d3a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924729"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>參數化命令與中介 COMPUTE 命令
一般參數化圖形 APPEND 命令有一個子句，它會使用查詢命令建立父**記錄集**，而另一個子句會使用參數化查詢命令建立子**記錄集**，也就是包含參數預留位置的命令（問號，"？"）。 產生的成形**記錄集**有兩個層級，其中父代會佔用上層，而子系會佔用較低的層級。  
  
 建立子**記錄集**的子句現在可能是任意數目的嵌套形狀計算命令，其中最深的嵌套命令包含參數化查詢。 產生的成形**記錄集**具有多個層級，其中父系會佔用最上層的層級，子系會佔用 lowermost 層級，而 shape 計算命令所產生的任意數目的**記錄集會**佔用仲介層級。  
  
 這項功能的典型用法是叫用 shapeCOMPUTE 命令的彙總函式和群組功能，以建立具有子**記錄集**相關分析資訊的中間**記錄集**物件。 此外，因為這是參數化圖形命令，所以每次存取父系的章節資料行時，可能會抓取新的子**記錄集**。 由於仲介層級衍生自子系，因此也會重新計算。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
