# syntax=docker/dockerfile:1

################################################################################
# Build Stage
################################################################################

FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:6.0-alpine AS build
ARG TARGETARCH

COPY . /source

WORKDIR /source/src

# Build the application with architecture-specific runtime
# Using a cache mount for NuGet packages to improve build performance
RUN --mount=type=cache,id=nuget,target=/root/.nuget/packages \
    dotnet publish -a ${TARGETARCH/amd64/x64} --use-current-runtime --self-contained false -o /app
    
################################################################################
# Runtime Stage
################################################################################

FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine AS final
WORKDIR /app

# Copy published application files from the build stage
COPY --from=build /app .

# Add a non-privileged user to run the application
ARG UID=10001
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "${UID}" \
    appuser
    
USER appuser

EXPOSE 80

ENTRYPOINT ["dotnet", "myWebApp.dll"]