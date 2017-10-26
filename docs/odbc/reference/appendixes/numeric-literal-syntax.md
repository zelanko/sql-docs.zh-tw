---
title: "數值常值的語法 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64a772d8a04015060aa717e4153bf6f36e5b74de
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="numeric-literal-syntax"></a>數值常值的語法
在 ODBC 中的數值常值會使用下列語法：  
  
 *數值常值*:: =*簽署數值常值 &#124; 不帶正負號數值常值*  
  
 *帶正負號數值常值*:: = [*登*]*不帶正負號數值常值*  
  
 *不帶正負號數值常值*:: =*精確數值常值 &#124; 近似數值常值*  
  
 *精確數值常值*:: =*不帶正負號整數*[*期間*[*不帶正負號整數*]] *&#124; 期間的不帶正負號整數*  
  
 *符號*:: =*加號 &#124; 減號*  
  
 *近似數值常值*:: =*尾數 E 指數*  
  
 *尾數*:: =*精確數值常值*  
  
 *指數*:: =*帶正負號整數*  
  
 *帶正負號整數*:: = [*登*]*不帶正負號整數*  
  
 *不帶正負號整數*:: =*位數...*  
  
 *加號*:: =*+*  
  
 *負號*:: =-  
  
 *數字*:: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *期間*:: =。

