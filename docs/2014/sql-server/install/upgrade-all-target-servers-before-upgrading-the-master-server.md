---
title: 升級所有目標伺服器，然後再升級主要伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d0df73fdfa1ebbaa84b0fb11519698351a78ffdc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218668"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>先升級所有目標伺服器後再升級主要伺服器
  升級主要伺服器之前，請先升級所有設定為目標伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 若要在多伺服器環境中自動化管理，您至少必須有一個主要伺服器和一個目標伺服器。 主要伺服器會將作業散發到目標伺服器，並接收目標伺服器傳回的事件。 對於目標伺服器上執行的作業，主要伺服器也會儲存其作業定義的集中副本。  
  
 如果目前的伺服器設定為主要伺服器，請先升級所有目標伺服器，然後再升級主要伺服器。  
  
## <a name="corrective-action"></a>更正動作  
 如果您無法在升級主要伺服器之前升級所有目標伺服器，就必須在升級之後，脫離所有目標伺服器並重新編列它們。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜將整個企業的管理自動化＞、＜如何：使目標伺服器脫離主要伺服器＞和＜如何：將目標伺服器編列至主要伺服器＞。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
