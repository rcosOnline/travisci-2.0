FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["testapi3.0/testapi3.0.csproj", "testapi3.0/"]
RUN dotnet restore "testapi3.0/testapi3.0.csproj"
COPY . .
WORKDIR "/src/testapi3.0"
RUN dotnet build "testapi3.0.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "testapi3.0.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testapi3.0.dll"]