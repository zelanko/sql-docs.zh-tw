---
title: 步驟 1:設定 Ruby 開發的開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67992466"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步驟 1:設定 Ruby 開發的開發環境
您必須搭配必要條件設定您的開發環境，才能使用 Ruby Driver for SQL Server 開發應用程式。    
  
請注意，Ruby 驅動程式會使用預設在 SQL Server 和 Azure SQL Database 中啟用的 TDS 通訊協定。  不需要進行其他組態設定。  
  
  
## <a name="windows"></a>Windows  
  
1.  **下載 Ruby 安裝程式**  
如果您的電腦沒有 Ruby，請加以安裝。 針對 Ruby 的新使用者，建議您使用 Ruby 2.2.X 安裝程式。 這些安裝程式能提供穩定的語言，以及相容且更新的詳盡套件 (gem) 清單。 移至 [Ruby 下載頁面](https://rubyinstaller.org/downloads/) \(英文\) 並下載適當的 2.1.x 安裝程式。 例如，如果您是在 64 位元的電腦上，請下載 Ruby 2.1.6 (x64) 安裝程式。   
  
2.  **安裝 Ruby**  
下載安裝程式之後，請執行下列動作：  
a. 按兩下檔案以啟動安裝程式。  
b. 選取您的語言，並同意條款。  
c.  在安裝設定畫面上，請同時選取 [Add Ruby executables to your PATH] \(將 Ruby 可執行檔新增至您的路徑\) 和 [Associate .rb and .rbw files with this Ruby installation] \(將 .rb 和 .rbw 檔案與此 Ruby 安裝相關聯\) 旁邊的核取方塊。  
  
3.  **下載 Ruby DevKit**  
從 RubyInstaller 頁面下載 DevKit  
  
4.  **安裝 Ruby DevKit**  
下載完成之後，請執行下列動作：  
a. 按兩下該檔案。 系統會詢問您將檔案解壓縮的位置。  
b. 按一下 [...] 按鈕，然後選取 "C:\DevKit"。 您可能需要先按一下 [建立新資料夾] 來建立此資料夾。  
c. 按一下 [確定]，然後按一下 [Extract] \(解壓縮\) 以將檔案解壓縮。  
  
5. **開啟 cmd.exe**  
  
6. **初始化 Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **安裝 TinyTDS gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **開啟終端機**  
  
2. **安裝 Ruby Version Manager (rvm) 和必要條件**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **使用 rvm 來安裝 Ruby**  
例如，安裝 Ruby 2.3.0 版：  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;確定上一個命令的輸出指出您正在執行 2.3.0 版。  
  
4.  **安裝 FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安裝 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
請注意，Mac OS X 已經預先安裝 Ruby，因為該 OS 具有相依性。    
  
1.  **開啟終端機**  
  
2. **安裝 Homebrew 套件管理員**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **安裝 FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **安裝 TinyTDS gem**  
```  
> gem install tiny_tds  
```
