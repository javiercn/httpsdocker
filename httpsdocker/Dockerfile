FROM microsoft/aspnetcore:2.1.0-preview1-bionic AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/aspnetcore-build:2.1.0-preview1-bionic AS build
WORKDIR /src
COPY httpsdocker.sln ./
COPY httpsdocker/httpsdocker.csproj httpsdocker/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/httpsdocker
RUN dotnet build httpsdocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish httpsdocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "httpsdocker.dll"]
