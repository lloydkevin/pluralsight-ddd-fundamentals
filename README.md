# Pluralsight DDD Fundamentals Sample

Sample code for the Pluralsight DDD Fundamentals course (coming soon) by Julie Lerman and Steve "ardalis" Smith. If you are looking for the .NET Framework sample from [the original 2014 DDD Fundamentals course](https://app.pluralsight.com/library/courses/domain-driven-design-fundamentals), it's available as the [ddd-vet-clinic sample](https://github.com/ardalis/ddd-vet-sample).

## Give a Star! :star:

If you like or are using this project to learn, please give it a star. Thanks!

## Running the Sample

The easiest way to run the sample is using docker. Download the source and run this command from the root folder:

```powershell
docker-compose build
docker-compose up
```

This will start RabbitMQ (for messaging between apps) and build and run each of the applications involved in the sample:

- FrontDesk.Api
- FrontDesk.Blazor
- ClinicManagement.Api
- ClinicManagement.Blazor
- VetClinicPublic

It also adds the following supporting containers:

- RabbitMQ with Management
- FrontDesk SQL Server
- ClinicManagement SQL Server
- Test Mailserver (Papercut)

Once running, you should be able to access the various apps using localhost (HTTP not HTTPS because of [Kestrel configuration restrictions](https://docs.microsoft.com/en-us/aspnet/core/security/docker-compose-https)) and the following ports (you can also find these bindings in the docker-compose.yml file):

| Service (in docker)            | Localhost Port | Visual Studio Port |
|--------------------------------|---------------:|-------------------:|
| FrontDesk (main app)           |           5100 |               5150 |
| ClinicManagement               |           6100 |               6150 |
| VetClinicPublic                |           7100 |               7150 |
| FrontDesk API / Swagger        |           5200 |               5250 |
| ClinicManagement API / Swagger |           6200 |               6250 |
| RabbitMQ Management            |          15673 |              15672 |
| RabbitMQ Service               |           5673 |              15673 |
| Papercut Management            |          37409 |              37408 |
| Papercut SMTP                  |           2525 |                 25 |

### Visual Studio

Running the sample from Visual Studio requires some additional setup. You will need to run multiple solutions side by side. You will also need to run RabbitMQ, ideally as a docker image, which you can so using this command:

```powershell
docker run --rm -it --hostname ddd-sample-rabbit -p 15672:15672 -p 5672:5672 rabbitmq:3-management
```

You should be able to open [localhost:15672](http://localhost:15672/#/) to view RabbitMQ management interface (login as guest/guest).

![rabbitmq management app](https://user-images.githubusercontent.com/782127/112649139-8a943b00-8e20-11eb-8bd5-1bfb15a9a90d.png)

When new appointments are created, confirmation emails are sent out to clients. Start a test mailserver using this command ([learn more](https://ardalis.com/configuring-a-local-test-email-server/)):

```powershell
docker run --name=papercut -p 25:25 -p 37408:37408 jijiechen/papercut:latest
```

You should be able to open [localhost:37408](http://localhost:37408) to view Papercut test mailserver management interface, where sent emails will appear.

![Papercut management app](https://user-images.githubusercontent.com/782127/112649314-b4e5f880-8e20-11eb-92d3-b120165847e6.png)

## Architecture Notes

## Deveoper Notes

## Credits

This sample is from [Julie Lerman](https://www.pluralsight.com/authors/julie-lerman) and [Steve Smith](https://www.pluralsight.com/authors/steve-smith)'s Pluralsight course. The original sample was written for .NET Framework by Steve. The current .NET 5 version was initially ported with the help of [Shady Nagy](https://twitter.com/ShadyNagy_). Progress Software provided the [Blazor Scheduler control](https://www.telerik.com/blazor-ui/scheduler) used to display the clinic's schedule. Additional credits include:

- TBD
