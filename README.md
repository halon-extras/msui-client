# MSUI client plugin

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-msui-client
```

### RHEL

```
yum install halon-extras-msui-client
```

## Configure MSUI

### Prerequisities

* ansible

Check out [MSUI documentation](https://docs.halon.io/msui/history.html) on how to configure MSUI.

## HSL client

The `msui` class needs to be [imported](https://docs.halon.io/hsl/structures.html#import) from the `extras://msui-client` module path.

### smtpd-app.yaml

```
scripting:
  files:
    - id: msui-config.yaml
      path: /etc/halon/msui-config.yaml
```

## msui()

The msui class.

**Returns**: class object.

**Example**

```
import { msui } from "extras://msui-client";

$msui = msui();
```

## domainExist(domain)

**Params**

This function returns `true` or `false` if a domain exists or not.

* domain `string` Fully-qualified domain name

**Returns**: `boolean``

**Example**

```
if ($msui->domainExist("example.com"))
{
  echo "Found";
}
else
{
  echo "No domain found";
}
```

## getDomain(domain)

**Params**

* domain `string` Fully-qualified domain name

**Returns**: `array`

**Example**

```
$domain = $msui->getDomain("example.com");

if ($domain)
{
  $destination = [
    "host" => $domain["transport"]["destination"][0]["hostname"],
    "port" => $domain["transport"]["destination"][0]["port"] ?? 25
  ];
}
```

## getDomainSettings(domain)

**Params**

* domain `string` Fully-qualified domain name

**Returns**: `array`

**Example**

```
$settings = $msui->getDomainSettings("example.com");

if ($settings["dkim"])
{
  $mail->signDKIM($settings["dkim"]["selector"], "example.com", $settings["dkim"]["privatekey"]);
}
```

## getUser(email)

**Params**

* email `string` E-mail address

**Returns**: `array`

**Example**

```
$settings = $msui->getUser("user@example.com");
```

## getUserSettings(email)

**Params**

* email `string` E-mail address

**Returns**: `array`

**Example**

```
$settings = $msui->getUserSettings("user@example.com");

if ($settings["allowlist"])
{
  if (array_includes($connection["remoteip"], $settings["allowlist"]))
  {
    Accept();
  }
}
```

## getSetting(id)

**Params**

* id `string` Settings identifier

**Returns**: `array`

**Example**

```
$settings = $msui->getSetting("relaylist");

if ($settings["domains"])
{
  foreach ($settings["domains"] as $domain => $value)
  {
    if (array_includes($connection["remoteip"], $value))
    {
      Accept();
    }
  }
}
```
