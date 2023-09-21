FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["QuizFrontend/QuizFrontend.csproj", "QuizFrontend/"]
RUN dotnet restore "QuizFrontend/QuizFrontend.csproj"
COPY . .
WORKDIR "/src/QuizFrontend"
RUN dotnet build "QuizFrontend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "QuizFrontend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "QuizFrontend.dll"]
