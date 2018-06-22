---
title: 管理交易 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, transactions
- XMLA, transactions
- explicit transactions [XMLA]
- implicit transactions
- transactions [XML for Analysis]
- rolling back transactions, XMLA
- reference counts [XML for Analysis]
- committing transactions
- starting transactions
ms.assetid: f5112e01-82f8-4870-bfb7-caa00182c999
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 84ec16569d7e4118c159b7a611cba9d711b9d761
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022033"
---
# <a name="managing-transactions-xmla"></a>管理交易 (XMLA)
  每個 XML for Analysis (XMLA) 命令傳送至執行個體[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]目前隱含或明確工作階段上的交易內容中執行。 若要管理每個交易，您使用[BeginTransaction](../xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../xmla/xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)命令。 透過使用這些命令，您可以建立隱含或是明確的交易、變更交易參考計數，以及開始、認可或是回復交易。  
  
## <a name="implicit-and-explicit-transactions"></a>隱含與明確交易。  
 交易是隱含或明確的：  
  
 **隱含交易**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立*隱含*為 xmla 命令，如果`BeginTransaction`命令未指定開始的交易。 如果命令成功，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 永遠都會認可隱含交易。而如果命令失敗，則會回復隱含交易。  
  
 **明確交易**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立*明確*交易如果`BeginTransaction`命令啟動的交易。 不過，如果傳送的是 `CommitTransaction` 命令，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只會認可明確交易。而如果傳送的是 `RollbackTransaction` 命令，則會回復明確交易。  
  
 此外，如果目前的工作階段在使用中交易完成之前就結束了目前的工作階段，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 則會回復隱含交易和明確交易。  
  
## <a name="transactions-and-reference-counts"></a>交易和參考計數  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為每個工作階段維護一個交易參考計數。 不過，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 並不支援巢狀交易，因為每個工作階段都只會維護一個使用中交易。 如果目前的工作階段沒有使用中交易，則會將交易參考計數設定為 0。  
  
 換句話說，每個 `BeginTransaction` 命令都會以一為單位遞增參考計數，而每個 `CommitTransaction` 命令則會以一為單位遞減參考計數。 如果 `CommitTransaction` 命令將交易計數設定為零，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會認可交易。  
  
 不過，`RollbackTransaction` 命令會回復使用中交易，不論交易參考計數目前的值為何。 換句話說，單一 `RollbackTransaction` 命令會回復使用中交易，不論傳送了多少 `BeginTransaction` 命令或是 `CommitTransaction` 命令，並將交易參考計數設定為零。  
  
## <a name="beginning-a-transaction"></a>開始交易  
 `BeginTransaction` 命令會在目前的工作階段上開始明確交易，並以一為單位為目前的工作階段遞增交易參考計數。 所有後續的命令都會視為在使用中交易內，直到已傳送足夠的 `CommitTransaction` 命令認可使用中交易，或是傳送單一 `RollbackTransaction` 命令來回復使用中交易為止。  
  
## <a name="committing-a-transaction"></a>認可交易  
 `CommitTransaction` 命令會認可在目前的工作階段上執行 `BeginTransaction` 命令之後所執行的命令結果。 每個 `CommitTransaction` 命令會為工作階段上的使用中交易遞減參考計數。 如果 `CommitTransaction` 命令將參考計數設定為零，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會認可使用中交易。 如果沒有使用中交易 (換句話說，目前工作階段的交易參考計數已經設定為零)，則 `CommitTransaction` 命令會產生錯誤。  
  
## <a name="rolling-back-a-transaction"></a>回復交易  
 `RollbackTransaction` 命令會回復在目前的工作階段上執行 `BeginTransaction` 命令之後所執行的命令結果。 不論目前交易參考計數為何，`RollbackTransaction` 命令都會回復使用中交易，並將交易參考計數設定為零。 如果沒有使用中交易 (換句話說，目前工作階段的交易參考計數已經設定為零)，則 `RollbackTransaction` 命令會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  