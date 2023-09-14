# Intro
O Homebridge é uma ferramenta que serve para criar pontes entre dispositivos inteligentes e o HomeKit, permitindo que dispositivos que não possuem suporte de fábrica possam ser adicionados e controlados através do app Home no iOS. As lâmpadas da Positivo não trazem suporte ao HomeKit de fábrica, mas podem ser adicionadas através do Homebridge, já que por trás das cenas a Positivo usa como base a tecnologia da fabricante chinesa Tuya.

O processo acontece da seguinte forma: primeiro é preciso baixar o app Tuya Smart, criar uma conta e adicionar sua lâmpada no dispositivo. Após isso é preciso criar uma conta de desnvolvimento IoT no site da Tuya, e utilizar o serviço de teste grátis para criar um projeto de desenvolvimento de nuvem, conectando com a sua conta Tuya Smart para conectar seus dispositivos com o projeto e obter alguns dados, como o DevID dos dispositivos. Após isso, basta inserir os dados no plugin da Tuya Platform no Homebridge. 

## Primeira etapa - Instalação do Homebridge.
- Instale o Homebridge conforme as instruções da [página oficial](https://github.com/homebridge/homebridge). 

## Segunda etapa - Adicionando os dispositivos no Tuya Smart.
- Baixe o app [Tuya Smart](https://apps.apple.com/br/app/tuya-smart/id1034649547?l) na App Store.
- Crie uma conta e adicione a sua lâmpada no aplicativo da mesma forma que você faria normalmente no app da Positivo.

## Terceira etapa - Criação do projeto no site da Tuya IoT
Esta etapa segue os passos do excelente tutorial criado por Max Isom, você pode conferir o original [aqui](https://github.com/codetheweb/tuyapi/blob/master/docs/SETUP.md)
1. Crie uma nova conta no site [iot.tuya.com](iot.tuya.com). Max recomenda selecionar United States como país para pular uma etapa de verificação.
2. Vá para Cloud -> Development. Você precisa "comprar" o Trial Plan para prosseguir. É gratuíto e não precisa inserir dados de cartão de crédito. Uma vez na aba Projects, clique em "Create". Dê um nome, seleciona "Smart Home" tanto no campo Industry quanto no campo Development Method, e insira o datacenter como Western America. Pule as opções de serviço na próxima tela. Depois de criar o projeto, clique nele para abrir. Os valores Access ID/Client ID e Access Secret/Client Secret serão necessários mais tarde.
3. Vá para Cloud -> Desenvolvimento -> (Nome do Projeto criado no passo anterior) -> Service API -> Go To Authorize (botão azul). Nesse painel você habilitará algumas APIs necessárias para o funcionamento do plugin no Homebridge. Para habilitar, basta clicar em "Free Trial", selecionar o nome do projeto e clicar em continue. Habilite as APIs "IoT Core", "Authorization Token Management", "Smart Home Basic Service" e Device Status Notification. No guia original do Max ele utiliza a API "Smart Home Scene Linkage", mas essa API aparentemente está deprecada. Para checar se as APIs estão habilitadas, abra Cloud -> Projects -> Projeto -> API.
4. Vá para Cloud -> Development -> Nome do Projeto. Clique na aba Devices, em seguida clique no botão "Link Tuya App account", e na próxima página mude a localização do datacenter no canto direito para "Western America".
5. Clique em Add App Account and escaneie o QR Code com o seu app Tuya Smart. Se houver erro de localização, mude o local do datacenter no canto direito. Se não houver outras opções, volte para a página de projetos, clique nos três pontos e edite o projeto para incluir outros datacenters. Depois, verifique se os dispositivos foram conectados abrindo a aba All Devices, dentro da aba Devices. Se houver falha nesse processo, será necessário seguir o tutorial do Max utilizando o Node.JS para conseguir essas informações.

## Quarta Etapa - Configurando o plugin da Tuya
1. Abra a dashboard do Homebridge através do endereço local. Abra a página Plugins e procure por Tuya. Para esse tutorial eu utilizei o plugin Homebridge Tuya Platform versão v1.7.0-beta-49.
2. Após a instalação, clique em Settings para começar a configurar o plugin. 
### Tuya Account Info:
- Project Type: Smart Home
- Endpoint URL: https://openapi.tuyaus.com
- Access ID: o Access ID do seu projeto criado no Tuya IoT
- Access Secret: o Access Secret do seu projeto criado no Tuya IoT
- Country Code: 55
- Username: seu email da conta do app Tuya Smart
- Password: a senha da conta do app Tuya Smart
- App: Tuya Smart
### Tuya Device
- ID: Device ID do dispositivo encontrado em Devices -> All Devices no projeto do Tuya IoT.
- Category: dj
- DP Code: 2
- Para inserir mais acessórios, clique em Add New Device Override e adicione os dados dos outros dispositivos.
3. Clique em Save e reinicie o Homebridge. Após isso, escaneie o código QR que aparece na dashboard para ligar o Homebridge ao app Home no iOS. Após isso, a lâmpada deve aparecer no aplicativo. Se não aparecer, tente remover o Bridge, reiniciar o servidor do Homebridge e adicionar novamente. Em ultimo caso reinstale o Homebridge e o plugin. 


