FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 50276
EXPOSE 44348

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY jenkin_pipeline_test/jenkin_pipeline_test.csproj jenkin_pipeline_test/
RUN dotnet restore jenkin_pipeline_test/jenkin_pipeline_test.csproj
COPY . .
WORKDIR /src/jenkin_pipeline_test
RUN dotnet build jenkin_pipeline_test.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish jenkin_pipeline_test.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "jenkin_pipeline_test.dll"]
