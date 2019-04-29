---
title: 負載平衡記錄在遠端伺服器上的套件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5c1da6e0663b5cc996a0af9706123a96c8c26e89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890670"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>遠端伺服器上負載平衡封裝的記錄
  當所有子封裝都使用相同的記錄提供者，而且全部寫入同一個目的地時，可以讓管理員較容易管理各種伺服器上執行之所有子封裝的記錄檔。 為所有子封裝建立共用記錄檔的其中一個方法，就是透過設定子封裝，使它們將事件記錄到 SQL Server 記錄提供者。 您可以將所有封裝設定成使用同一個資料庫、同一部伺服器，以及伺服器的同一個執行個體。  
  
 若要檢視記錄檔，管理員只需登入單一伺服器即可檢視所有子封裝的記錄檔。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何啟用封裝中記錄的資訊，請參閱 [在 SQL Server Data Tools 中啟用封裝記錄功能](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  
