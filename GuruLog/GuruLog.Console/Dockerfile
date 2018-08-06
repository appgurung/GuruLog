FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 10101
EXPOSE 44318

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY GuruLog.Console/GuruLog.Console.csproj GuruLog.Console/
RUN dotnet restore GuruLog.Console/GuruLog.Console.csproj
COPY . .
WORKDIR /src/GuruLog.Console
RUN dotnet build GuruLog.Console.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish GuruLog.Console.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GuruLog.Console.dll"]
