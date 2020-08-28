---
description: 參數化命令與中介 COMPUTE 命令
title: 使用中間計算命令參數化命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6870d6670bb0cda3db0d301621196121f2289cd8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980149"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>參數化命令與中介 COMPUTE 命令
一般參數化圖形附加命令具有使用查詢命令建立父 **記錄集** 的子句，以及使用參數化查詢命令建立子 **記錄集** 的另一個子句，也就是包含參數預留位置 (問號 "？" 的命令。) 。 產生的成形 **記錄集** 有兩個層級，其中父代占上層，而子系占較低的層級。  
  
 建立子 **記錄集** 的子句現在可以是任意數目的嵌套圖形計算命令，其中最深的嵌套命令包含參數化查詢。 產生的成形 **記錄集** 有多個層級，在此層級中，父系會佔用最上層層級、子系占 lowermost 層級，而圖形計算命令所產生的任意數目的 **記錄集會**佔用仲介層級。  
  
 這項功能的典型用途是叫用 shapeCOMPUTE 命令的彙總函式和群組能力，以建立包含子記錄**集**之分析資訊的仲介**記錄集**物件。 此外，因為這是參數化圖形命令，所以每次存取父系的章節資料行時，就可能會取出新的子 **記錄集** 。 因為仲介層級衍生自子系，所以也會重新計算。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
