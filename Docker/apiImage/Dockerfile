FROM buildpack-deps:jessie-curl as repo
RUN mkdir /usr/repo
WORKDIR /usr/repo

RUN apt-get update \
    && apt-get install unzip

# Download artefatos
RUN curl -s https://api.github.com/repos/pauloofmeta/calcsoft/releases/latest \
  | grep "browser_download_url.*calcsoftApi" \
  | cut -d ":" -f 2,3 \
  | tr -d \" \
  | wget -qi -
  
RUN unzip -a calcsoftApi.zip
RUN rm calcsoftApi.zip

FROM  microsoft/dotnet:2.1-aspnetcore-runtime AS final
WORKDIR /app
COPY --from=repo /usr/repo /app
EXPOSE 80
ENTRYPOINT ["dotnet", "CalcSoft.Api.dll"]