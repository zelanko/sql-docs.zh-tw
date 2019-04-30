---
title: 管理交易 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c85b1f9db4667c64bed7cf87189e48b507e5f75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63055073"
---
# <a name="managing-transactions-xmla"></a>管理交易 (XMLA)
  每個 XML for Analysis (XMLA) 命令傳送至執行個體[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上目前的隱含或明確工作階段之交易內容中執行。 若要管理每個交易，您使用[BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)， [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)，並[RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla)命令。 透過使用這些命令，您可以建立隱含或是明確的交易、變更交易參考計數，以及開始、認可或是回復交易。  
  
## <a name="implicit-and-explicit-transactions"></a>隱含與明確交易。  
 交易是隱含或明確的：  
  
 **隱含交易**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會建立*隱含*交易為 xmla 命令，如果**BeginTransaction**命令未指定開始的交易。 如果命令成功，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 永遠都會認可隱含交易。而如果命令失敗，則會回復隱含交易。  
  
 **明確交易**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會建立*明確*交易如果**BeginTransaction**命令會啟動的交易。 不過，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]只有在如果認可明確交易**CommitTransaction**命令傳送，且如果回復明確交易**RollbackTransaction**傳送命令。  
  
 此外，如果目前的工作階段在使用中交易完成之前就結束了目前的工作階段，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 則會回復隱含交易和明確交易。  
  
## <a name="transactions-and-reference-counts"></a>交易和參考計數  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為每個工作階段維護一個交易參考計數。 不過，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 並不支援巢狀交易，因為每個工作階段都只會維護一個使用中交易。 如果目前的工作階段沒有使用中交易，則會將交易參考計數設定為 0。  
  
 換句話說，每個**BeginTransaction**命令的參考計數遞增一，而每一個**CommitTransaction**命令遞減參考計數的其中一個。 如果**CommitTransaction**命令會將交易計數設定為零，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]認可交易。  
  
 不過， **RollbackTransaction**命令會回復交易參考計數目前的值為何使用中交易。 換句話說，單一**RollbackTransaction**命令會回復使用中的交易，無論多少**BeginTransaction**命令或**CommitTransaction**命令已傳送，並設定交易參考計數為零。  
  
## <a name="beginning-a-transaction"></a>開始交易  
 **BeginTransaction**命令開始明確交易目前的工作階段上，並針對目前的工作階段的交易參考計數遞增一。 所有後續的命令會被視為在使用中交易，直到足夠**CommitTransaction**命令傳送至使用中交易或單一認可**RollbackTransaction**命令傳送至回復使用中交易。  
  
## <a name="committing-a-transaction"></a>認可交易  
 **CommitTransaction**命令認可之後所執行的命令的結果**BeginTransaction**目前工作階段上執行。 每個**CommitTransaction**命令遞減參考計數的使用中交易的工作階段。 如果**CommitTransaction**命令會將參考計數設定為零，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]認可使用中交易。 如果沒有任何作用中交易 （換句話說，目前的工作階段的交易參考計數已經設為零）， **CommitTransaction**命令會產生錯誤。  
  
## <a name="rolling-back-a-transaction"></a>回復交易  
 **RollbackTransaction**命令會回復之後所執行的命令的結果**BeginTransaction**目前工作階段上執行。 **RollbackTransaction**命令回復使用中交易，不論目前的交易參考計數，並將交易參考計數設定為零。 如果沒有任何作用中交易 （換句話說，目前的工作階段的交易參考計數已經設為零）， **RollbackTransaction**命令會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
