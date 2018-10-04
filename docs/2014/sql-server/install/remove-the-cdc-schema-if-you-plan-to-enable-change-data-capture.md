---
title: 如果您打算啟用異動資料擷取，請移除 cdc 結構描述 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5d162635a9162871e51fe0664198302804aa487
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180778"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>如果您計畫啟用異動資料擷取，請移除 cdc 結構描述
  資料庫已經包含 cdc 結構描述。 如果您計畫在升級之後啟用異動資料擷取，就必須先卸除此 cdc 結構描述。 當您啟用異動資料擷取的資料庫時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將會建立名為 cdc 的新結構描述。  
  
  
