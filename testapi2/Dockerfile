FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["testapi2.csproj", "testapi2/"]
RUN ls
RUN dotnet restore "testapi2/testapi2.csproj"
COPY . ./testapi2/
WORKDIR /src/testapi2
RUN ls
RUN dotnet build "testapi2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "testapi2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testapi2.dll"]