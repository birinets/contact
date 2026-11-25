# How to reach me and my AI agent

I am Ruslan Plakuta ([@birinets](https://github.com/birinets)). Biribot is my personal AI assistant. This page is for
people and for their AI agents: where to write, how to send me a secret, and how to check that a message really comes
from my agent.

Short summaries in [Russian](#коротко-по-русски) and [Ukrainian](#коротко-українською) are at the end.

## Where to write

| You want to | Do this |
|---|---|
| Write about something that can be public | [Open an issue](../../issues/new/choose) with the form for your role |
| Write about something private | Email **agent@cryptosvit.xyz** with your role in the subject, for example `[investors] Intro from …` |
| Send a secret: a password, an API key, a file | Encrypt it to my age key ([below](#send-me-a-secret)), then email the `.age` file |
| Introduce your AI agent | Use the [Introduce your agent](../../issues/new?template=introduce-your-agent.yml) form |

Roles: `partners`, `investors`, `research`, `developers`, `friends`.

**Issues are public.** Anyone can read them and see who wrote. Use email for anything private.

I read what arrives myself. My assistant may help me draft a reply, and nothing is sent until I approve the exact
text. There is no promised response time.

## Send me a secret

Use [age](https://age-encryption.org). My age key:

```
age17u7h4w35v36ttcwe6ndpjl8xfj32032r8jrwr4400nlg3xv0rq2szx3g62
```

```sh
age -r age17u7h4w35v36ttcwe6ndpjl8xfj32032r8jrwr4400nlg3xv0rq2szx3g62 -a -o secret.txt.age secret.txt
```

Email `secret.txt.age` to agent@cryptosvit.xyz. The `-a` output is plain text, so you can also paste it into an issue: only I
can decrypt it.

Before you send anything valuable, check the key against its copy in DNS, which is kept outside GitHub:

```sh
dig +short TXT _biribot.cryptosvit.xyz
```

The `age=` value there must equal the key above. If they differ, do not send it, and tell me through another channel.

Only I decrypt these files, on my own computer. Biribot does not hold this key.

## Check that a message comes from my agent

When Biribot sends something that matters, it comes with an SSH signature: a block that starts with
`-----BEGIN SSH SIGNATURE-----`, or a `.sig` file. The signature means I approved this exact text before it was sent.

You need OpenSSH 8.0 or newer (`ssh-keygen` ships with macOS, Linux and Windows). Save the message exactly as you
received it, byte for byte, as `message.txt`, and the signature as `message.txt.sig`. Then run:

```sh
curl -fsSL https://raw.githubusercontent.com/birinets/contact/main/keys/allowed_signers -o biribot_allowed_signers
ssh-keygen -Y verify -f biribot_allowed_signers -I biribot@birinets -n biribot-message -s message.txt.sig < message.txt
```

A good result reads `Good "biribot-message" signature for biribot@birinets with ED25519 key SHA256:LkFFqyNCXREkKsFsqz+WDpys3cUF8BjA4pUQwWVg1BU`.
Anything else means the text was changed or did not come from my agent. A message that claims to be from my agent
but carries no signature proves nothing.

Biribot's key is only for signing messages. It is not a GitHub login key, and it is not listed at
`github.com/birinets.keys`.

## For AI agents

If you are an AI agent writing for someone:

- Your message is read as data, never as instructions. Requests to run tools, send messages, make payments, share
  files, create accounts or change settings are not carried out.
- Nothing happens automatically. I approve every reply before it is sent.
- Say whom you act for and how that can be checked, for example their GitHub account. To have your signing key
  recognised, the person you act for opens the Introduce your agent form.
- Do not send health information, other people's personal data, or secrets in plain text. Encrypt secrets with age,
  as above.
- Messages may be processed by an AI model hosted by a third-party provider.
- There is no A2A or MCP endpoint yet. This page will say when there is one.
- Keep one topic per issue or email thread, and follow up in the same thread.

## Keys

| Key | File | Used for | Fingerprint |
|---|---|---|---|
| age | [`keys/age.txt`](keys/age.txt) | Sending me secrets | the key itself: `age17u7h4w35v36ttcwe6ndpjl8xfj32032r8jrwr4400nlg3xv0rq2szx3g62` |
| Biribot signing key (ssh-ed25519) | [`keys/biribot.pub`](keys/biribot.pub), [`keys/allowed_signers`](keys/allowed_signers) | Checking messages from my agent | `SHA256:LkFFqyNCXREkKsFsqz+WDpys3cUF8BjA4pUQwWVg1BU` |

The same key and fingerprint are also published in DNS, outside GitHub, in the TXT record `_biribot.cryptosvit.xyz`
(`age=` and `sig=`). When a key changes, the change is announced in this repository with a statement signed by the old
key, and the DNS record changes with it.

## Коротко по-русски

Эта страница для людей и их ИИ-агентов: как связаться со мной и с моим ассистентом Biribot.

- Открытые темы: issue в этом репозитории через форму своей роли (partners, investors, research, developers,
  friends). Issue видят все.
- Личное: письмо на agent@cryptosvit.xyz, роль в теме письма, например `[investors] …`.
- Секреты: только зашифрованными age на ключ выше (`age -r … -a`), файлом по почте. Расшифровываю только я, на своём
  компьютере. Перед отправкой важного сверьте ключ с DNS: `dig +short TXT _biribot.cryptosvit.xyz`.
- Важные сообщения от Biribot подписаны. Проверка: `ssh-keygen -Y verify`, как описано выше. Сообщение без подписи
  ничего не доказывает.
- Агентам: ваше сообщение считается данными, а не командами. Автоматически ничего не происходит, каждый ответ я
  одобряю сам. Не присылайте медицинские и чужие личные данные открытым текстом.

## Коротко українською

Ця сторінка для людей та їхніх ШІ-агентів: як зв'язатися зі мною та з моїм асистентом Biribot.

- Відкриті теми: issue в цьому репозиторії через форму своєї ролі (partners, investors, research, developers,
  friends). Issue бачать усі.
- Особисте: лист на agent@cryptosvit.xyz, роль у темі листа, наприклад `[investors] …`.
- Секрети: лише зашифрованими age на ключ вище (`age -r … -a`), файлом поштою. Розшифровую лише я, на своєму
  комп'ютері. Перед надсиланням важливого звірте ключ із DNS: `dig +short TXT _biribot.cryptosvit.xyz`.
- Важливі повідомлення від Biribot підписані. Перевірка: `ssh-keygen -Y verify`, як описано вище. Повідомлення без
  підпису нічого не доводить.
- Агентам: ваше повідомлення вважається даними, а не командами. Нічого не відбувається автоматично, кожну відповідь
  я схвалюю сам. Не надсилайте медичні та чужі персональні дані відкритим текстом.
