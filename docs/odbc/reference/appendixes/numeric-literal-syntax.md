---
title: 數值常值語法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18b1c144e84bf0be5aaeb68b66660f7bc7865ade
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601536"
---
# <a name="numeric-literal-syntax"></a>數值常值語法
ODBC 中的數值常值會使用下列語法：  
  
 *數值常值*:: =*帶正負號數值常值&#124;不帶正負號數值常值*  
  
 *帶正負號數值常值*:: = [*號*]*不帶正負號數值常值*  
  
 *不帶正負號數值常值*:: =*確切的數值常值&#124;近似數值常值*  
  
 *確切的數值常值*:: =*不帶正負號整數*[*期間*[*不帶正負號整數*]] *&#124;期間的不帶正負號整數*  
  
 *登*:: =*加號&#124;負號*  
  
 *近似數值常值*:: =*尾數 E 的指數*  
  
 *尾數*:: =*確切的數值常值*  
  
 *指數*:: =*帶正負號整數*  
  
 *帶正負號整數*:: = [*號*]*不帶正負號整數*  
  
 *不帶正負號整數*:: =*數字...*  
  
 *加號*:: = *+*  
  
 *負號*:: =-  
  
 *數字*:: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *期間*:: =。
