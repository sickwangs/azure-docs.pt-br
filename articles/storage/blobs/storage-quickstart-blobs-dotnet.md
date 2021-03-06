---
title: "Guia de início rápido do Azure – Transferir objetos para/do Armazenamento de Blobs do Azure usando o .NET | Microsoft Docs"
description: Aprenda rapidamente a transferir objetos de/para o Armazenamento de Blobs do Azure usando o .NET
services: storage
documentationcenter: storage
author: tamram
manager: jeconnoc
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 11/10/2017
ms.author: tamram
ms.openlocfilehash: ca4cb2dea9cdd2e46c3aef042e525acdfc09de8e
ms.sourcegitcommit: 8aa014454fc7947f1ed54d380c63423500123b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2017
---
# <a name="transfer-objects-tofrom-azure-blob-storage-using-net"></a>Transferir objetos de/para o Armazenamento de Blobs do Azure usando o .NET

Neste guia de início rápido, você aprende a usar a biblioteca de clientes do .NET para o Armazenamento do Azure para carregar, baixar e listar blobs de bloco em um contêiner.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este guia de início rápido, instale o [Visual Studio 2017](https://www.visualstudio.com/visual-studio-homepage-vs.aspx) com a seguinte carga de trabalho:

- **Desenvolvimento do Azure**

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [storage-quickstart-tutorial-create-account-portal](../../../includes/storage-quickstart-tutorial-create-account-portal.md)]

## <a name="download-the-sample-application"></a>Baixar o aplicativo de exemplo

O aplicativo de exemplo usado neste guia de início rápido é um aplicativo de console básico. 

Use o [git](https://git-scm.com/) para baixar uma cópia do aplicativo para seu ambiente de desenvolvimento. 

```bash
git clone https://github.com/Azure-Samples/storage-blobs-dotnet-quickstart.git
```

Este comando clona o repositório para sua pasta do git local. Para abrir a solução do Visual Studio, procure a pasta storage-blobs-dotnet-quickstart, abra-a e clique duas vezes em storage-blobs-dotnet-quickstart.sln. 

## <a name="configure-your-storage-connection-string"></a>Configurar a cadeia de conexão de armazenamento

No aplicativo, você deve fornecer a cadeia de conexão para sua conta de armazenamento. Abra o arquivo `app.config` no Gerenciador de Soluções no Visual Studio. Localize a entrada `StorageConnectionString`. Para **value**, substitua todo o valor da cadeia de conexão pelo que você salvou do Portal do Azure. Seu `storageConnectionString` deve ser semelhante ao seguinte:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;
    AccountName=<NameHere>;
    AccountKey=<KeyHere>" />
  </appSettings>
</configuration>
```

## <a name="run-the-sample"></a>Execute o exemplo

Este exemplo cria um arquivo de teste em Meus Documentos, carrega-o para o Armazenamento de Blobs, lista os blobs no contêiner e baixa o arquivo com um novo nome para que você possa comparar o arquivo novo com antigo. 

Execute o exemplo pressionando F5. Ele mostra a saída em uma janela de console semelhante a esta: 

```
Temp file = C:\Users\azureuser\Documents\QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8.txt
Uploading to Blob storage as blob 'QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8.txt'
List blobs in container.
https://mystorage.blob.core.windows.net/quickstartblobs/QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8.txt
Downloading blob to C:\Users\azureuser\Documents\QuickStart_cbd5f95c-6ab8-4cbf-b8d2-a58e85d7a8e8_DOWNLOADED.txt
```

Quando você pressiona qualquer tecla para continuar, ele exclui o contêiner de armazenamento e os arquivos. Antes de continuar, verifique se os dois documentos estão em MyDocuments. Você pode abri-los e ver que eles são idênticos. Copie a URL para o blob fora da janela do console e cole-a em um navegador para exibir o conteúdo do arquivo no Armazenamento de Blobs.

Você também pode usar uma ferramenta como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para exibir os arquivos no Armazenamento de Blobs. O Gerenciador de Armazenamento do Azure é uma ferramenta gratuita de multiplataforma que permite que você acesse as informações da sua conta de armazenamento. 

Depois de verificar os arquivos, pressione qualquer tecla para concluir a demonstração e excluir os arquivos de teste. Agora que você sabe o que o exemplo faz, abra o arquivo Program.cs para examinar o código. 

## <a name="understand-the-sample-code"></a>Entender o código de exemplo

Em seguida, vamos percorrer o código de exemplo para que você possa entender como ele funciona.

### <a name="get-references-to-the-storage-objects"></a>Obter referências a objetos de armazenamento

A primeira coisa a fazer é criar as referências aos objetos usados para acessar e gerenciar o Armazenamento de Blobs. Esses objetos dependem uns dos outros, cada um é usado pelo próximo na lista.

* Crie uma instância do objeto **CloudStorageAccount** apontando para a conta de armazenamento. 

* Crie uma instância do objeto **CloudBlobClient**, que aponta para o serviço Blob na sua conta de armazenamento. 

* Crie uma instância do objeto **CloudBlobContainer** que representa o contêiner que você está acessando. Os contêineres são usados para organizar seus blobs da mesma forma que você usa pastas no seu computador para organizar seus arquivos.

Assim que tiver o **CloudBlobContainer**, será possível criar uma instância do objeto **CloudBlockBlob**, que aponta para o blob específico em que você está interessado e realizar a operação de upload, download, cópia etc.

> [!IMPORTANT]
> Os nomes de contêiner devem estar em minúsculas. Consulte [Naming and Referencing Containers, Blobs, and Metadata](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata) (Nomenclatura e referência de contêineres, blobs e metadados) para obter mais informações sobre nomes de contêiner e de blobs.

Nesta seção, você cria uma instância de objetos, cria um novo contêiner e, em seguida, define as permissões no contêiner para que os blobs sejam públicos e possam ser acessados com apenas uma URL. O contêiner é chamado de **quickstartblobs**. 

Este exemplo usa **CreateIfNotExists** porque queremos criar um novo contêiner cada vez que a amostra for executada. Em um ambiente de produção em que você usa o mesmo contêiner em um aplicativo, é uma prática recomendada chamar **CreateIfNotExists** somente uma vez. Como alternativa, é possível criar o contêiner antecipadamente para não precisar criá-lo no código.

```csharp
// Create a CloudStorageAccount instance pointing to your storage account.
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the CloudBlobClient that is used to call the Blob Service for that storage account.
CloudBlobClient cloudBlobClient = storageAccount.CreateCloudBlobClient();

// Create a container called 'quickstartblobs'. 
CloudBlobContainer cloudBlobContainer = 
    cloudBlobClient.GetContainerReference("quickstartblobs");
await cloudBlobContainer.CreateIfNotExistsAsync();

// Set the permissions so the blobs are public. 
BlobContainerPermissions permissions = new BlobContainerPermissions();
permissions.PublicAccess = BlobContainerPublicAccessType.Blob;
await cloudBlobContainer.SetPermissionsAsync(permissions);
```

### <a name="upload-blobs-to-the-container"></a>Carregar blobs para o contêiner

O Armazenamento de Blobs dá suporte a blobs de blocos, blobs de acréscimo e blobs de páginas. Os blobs de bloco são utilizados com mais frequência e é o que é usado nesse guia de início rápido. 

Para carregar um arquivo em um blob, obtenha uma referência para o blob no contêiner de destino. Após obter a referência de blob, você pode carregar dados nele usando [CloudBlockBlob.UploadFromFileAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromfileasync). Essa operação cria o blob, se ele ainda não existir, ou o substitui, se ele já existir.

O código de exemplo cria um arquivo local a ser usado para o upload e para o download, armazenando o arquivo a ser carregado como **fileAndPath** e o nome do blob no **localFileName**. O exemplo a seguir carrega o arquivo para seu contêiner chamado **quickstartblobs**.

```csharp
// Create a file in MyDocuments to test the upload and download.
string localPath = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
string localFileName = "QuickStart_" + Guid.NewGuid().ToString() + ".txt";
string fileAndPath = Path.Combine(localPath, localFileName);
File.WriteAllText(fileAndPath, "Hello, World!");

//Upload the file.
CloudBlockBlob blockBlob = container.GetBlockBlobReference(localFileName);
await blockBlob.UploadFromFileAsync(fileAndPath);
```

Há vários métodos de upload que você pode usar com o Armazenamento de Blobs. Por exemplo, se você tiver um fluxo de memória, poderá usar o método UploadFromStreamAsync em vez de UploadFromFileAsync. 

Blobs de bloco podem ser qualquer tipo de arquivo binário ou de texto. Os blobs de páginas são usados principalmente para os arquivos VHD usados auxiliar as VMs IaaS. Os blobs de acréscimo são usados para registro em log, como quando você quer gravar em um arquivo e depois adicionar mais informações. A maioria dos objetos armazenados no Armazenamento de Blobs são blobs de blocos.

### <a name="list-the-blobs-in-a-container"></a>Listar os blobs em um contêiner

Obtenha uma lista de arquivos no contêiner usando [CloudBlobContainer.ListBlobsSegmentedAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobssegmentedasync). O código a seguir recupera a lista de blobs e a percorre, mostrando os URIs dos blobs encontrados. Você pode copiar o URI da janela de comando e colá-lo em um navegador para exibir o arquivo.

Se você tiver 5.000 blobs ou menos no contêiner, todos os nomes de blob serão recuperados em uma chamada para ListBlobsSegmentedAsync. Se você tiver mais de 5.000 blobs no contêiner, o serviço recuperará a lista em conjuntos de 5.000 até que todos os nomes de blob tenham sido recuperados. Portanto, na primeira vez que essa API é chamada, ela retorna os primeiros 5.000 nomes de blobs e um token de continuação. Na segunda vez, você fornece o token e o serviço recupera o próximo conjunto de nomes de blobs e assim por diante até que o token de continuação seja nulo, o que indica que todos os nomes de blobs foram recuperados. 

```csharp
// List the blobs in the container.
Console.WriteLine("List blobs in container.");
BlobContinuationToken blobContinuationToken = null;
do
{
    var results = await cloudBlobContainer.ListBlobsSegmentedAsync(null, blobContinuationToken);
    foreach(IListBlobItem item in results.Results)
    {
        Console.WriteLine(item.Uri);
    }
} while (blobContinuationToken != null);
```

### <a name="download-blobs"></a>Baixar blobs

Baixe os blobs para o disco local usando [CloudBlob.DownloadToFileAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadtofileasync).

O código a seguir baixa o blob carregado em uma seção anterior, adicionando um sufixo de "_DOWNLOADED" ao nome do blob para que você possa ver ambos os arquivos no disco local. 

```csharp
// Download blob. In most cases, you would have to retrieve the reference
//   to cloudBlockBlob here. However, we created that reference earlier, and 
//   haven't changed the blob we're interested in, so we can reuse it. 
// First, add a _DOWNLOADED before the .txt so you can see both files in MyDocuments.
string fileAndPath2 = fileAndPath.Replace(".txt", "_DOWNLOADED.txt");
Console.WriteLine("Downloading blob to {0}", fileAndPath2);
await cloudBlockBlob.DownloadToFileAsync(fileAndPath2, FileMode.Create);
```

### <a name="clean-up-resources"></a>Limpar recursos

Se você não precisar mais dos blobs carregados neste guia de início rápido, poderá excluir o contêiner inteiro usando [CloudBlobContainer.DeleteAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteasync). Também exclua os arquivos criados se eles não forem mais necessários.

```csharp
await cloudBlobContainer.DeleteAsync();
File.Delete(fileAndPath);
File.Delete(fileAndPath2);    
```

## <a name="next-steps"></a>Próximas etapas

Nesse guia de início rápido, você aprendeu a transferir arquivos entre o disco local e Armazenamento de Blobs do Azure usando o .NET. Para saber mais sobre como trabalhar com o Armazenamento de Blobs, prossiga para as instruções do Armazenamento de Blobs.

> [!div class="nextstepaction"]
> [Instruções de operações do Armazenamento de Blobs](storage-dotnet-how-to-use-blobs.md)

Para obter exemplos de código adicionais do Armazenamento do Azure que podem ser baixados e executados, consulte a lista de [amostras do Armazenamento do Azure que usam o .NET](../common/storage-samples-dotnet.md).

Para obter mais informações sobre o Gerenciador de Armazenamento e os Blobs, consulte [Gerenciar os recursos de Armazenamento de Blobs do Azure com o Gerenciador de Armazenamento](../../vs-azure-tools-storage-explorer-blobs.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).
