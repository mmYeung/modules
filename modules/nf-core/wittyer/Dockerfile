FROM mcr.microsoft.com/dotnet/sdk:9.0@sha256:4dceb990b7f76ae0b2f4e4fb1ac3485c3a354fb9fdaed767edb7590273508602 as builder

ADD https://github.com/Illumina/witty.er.git#v0.5.2 /src

WORKDIR /src/Wittyer
RUN dotnet publish -f net6.0 -r linux-x64 -c Release -o /output \
    && chmod +x /output/Wittyer

FROM mcr.microsoft.com/dotnet/runtime:9.0@sha256:9e854639a48c75547744c0c9c9bea3d28b6d4cc65daf9ed00fc290a87cb2f04d

LABEL git_repository=https://git.illumina.com/DASTE/Ilmn.Das.App.Wittyer.git
WORKDIR /opt/Wittyer
RUN apt-get -y update && apt-get -y install tabix libunwind8 openssl procps
COPY --from=builder /output /opt/Wittyer
