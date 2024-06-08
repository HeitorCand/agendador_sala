# Documentacão do projeto

## Introdução

Este projeto visa criar um sistema onde os alunos possam agendar as salinhas de uso comum no campus. O sistema permitirá que os alunos realizem agendamentos, cancelem agendamentos, e visualizem a disponibilidade das salas.

## Funcionalidades

- Agendamento de salas: Permite que os alunos agendem uma sala para uso.
- Cancelamento de agendamento: Permite que os alunos cancelem um agendamento existente.
- Visualização de salas disponíveis: Permite que os alunos vejam quais salas estão disponíveis para agendamento.
- Visualização de salas ocupadas: Permite que os alunos vejam quais salas estão atualmente ocupadas.
- Visualização de salas agendadas: Permite que os alunos vejam uma lista de salas que já foram agendadas.

## Descobertas até agora

Foi descoberto que cada salinha possui um e-mail criado pelo time do INTELI, que pode ser utilizado para agendar a sala. Mas como descobrir esse e-mail?

Crie um evento no Google Calendar e adicione a salinha. Por padrão, ela não é sugerida, portanto, é necessário escrever "R" para que ela seja sugerida.

<img src="/outros/descobrirEmailCasinha.png">

Após isso, você receberá um e-mail automático da salinha recusando o agendamento. Neste e-mail, estará o e-mail da salinha.

<img src="/outros/salinhaRecusando.png">

Com essas informações, foi possível criar um script integrado com o Google Calendar que lê os eventos e cria novos eventos, podendo marcar as salinhas nesses eventos.

Arquivo: [Pagina de test google calendar](/Criar%20evento%20e%20Ler%20Eventos/index.html)

## Configurações Necessárias

O primeiro passo é adicionar as configurações de integração do Google Calendar no arquivo index.html. Essas configurações são obtidas no console do Google Cloud. Para realizar essa integração, é necessário criar um projeto no Google Cloud e ativar a API do Google Calendar.

```js
// Define as constantes necessárias para o uso da API do Google Calendar
const CLIENT_ID = "client_id";
const API_KEY = "Api_key";
```

Depois de realizar todas as configurações necessárias, é possível realizar a leitura dos eventos e a criação de novos eventos

## Modificação de Eventos

No momento, algumas funcionalidades da criação de eventos são mockadas. Para adicionar algumas configurações adicionais, é necessário realizar mudanças no código. Aqui está um exemplo de como modificar o evento que será criado:

### Exemplo de Código para Modificar Evento
```js
const event = {
  summary: eventName,
  location: eventLocation,
  description: "A chance to hear more about Google's developer products.",
  start: {
    dateTime: startDate.toISOString(),
    timeZone: brazilTimezone,
  },
  end: {
    dateTime: endDate.toISOString(),
    timeZone: brazilTimezone,
  },
  attendees: [
    //email de uma casinha
    { email: "c_1884ea6rtpl98gg6hdobm2htogeds@resource.calendar.google.com" },
  ],
  reminders: {
    useDefault: false,
    overrides: [
      { method: "email", minutes: 24 * 60 },
      { method: "popup", minutes: 10 },
    ],
  },
};
```

## Conclusão

É possível criar agendamentos com as salinhas, porém, a conta das salinhas possui um sistema de segurança que impede que qualquer pessoa adicione um evento diretamente. Portanto, o próximo passo seria solicitar ao time do INTELI para que eles criarem uma conta com as permissões necessárias para realizar testes. Posteriormente, será necessário definir medidas de segurança para garantir que apenas usuários autorizados possam criar eventos.