---
title: 如果您打算啟用變更資料捕獲，請移除 cdc 架構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: abdb33fa3d1ff022a65ed569f19d48bcf4468501
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059153"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>如果您計畫啟用異動資料擷取，請移除 cdc 結構描述
  資料庫已經包含 cdc 結構描述。 如果您計畫在升級之後啟用異動資料擷取，就必須先卸除此 cdc 結構描述。 當您啟用異動資料擷取的資料庫時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 將會建立名為 cdc 的新結構描述。  
  
  
