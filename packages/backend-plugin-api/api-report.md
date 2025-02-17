## API Report File for "@backstage/backend-plugin-api"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts
import { Config } from '@backstage/config';
import { Handler } from 'express';
import { Logger as Logger_2 } from 'winston';
import { PermissionAuthorizer } from '@backstage/plugin-permission-common';
import { PermissionEvaluator } from '@backstage/plugin-permission-common';
import { PluginCacheManager } from '@backstage/backend-common';
import { PluginDatabaseManager } from '@backstage/backend-common';
import { PluginEndpointDiscovery } from '@backstage/backend-common';
import { PluginTaskScheduler } from '@backstage/backend-tasks';
import { TokenManager } from '@backstage/backend-common';
import { TransportStreamOptions } from 'winston-transport';
import { UrlReader } from '@backstage/backend-common';

// @public (undocumented)
export interface BackendFeature {
  // (undocumented)
  id: string;
  // (undocumented)
  register(reg: BackendRegistrationPoints): void;
}

// @public (undocumented)
export interface BackendModuleConfig<TOptions> {
  // (undocumented)
  moduleId: string;
  // (undocumented)
  pluginId: string;
  // (undocumented)
  register(
    reg: Omit<BackendRegistrationPoints, 'registerExtensionPoint'>,
    options: TOptions,
  ): void;
}

// @public (undocumented)
export interface BackendPluginConfig<TOptions> {
  // (undocumented)
  id: string;
  // (undocumented)
  register(reg: BackendRegistrationPoints, options: TOptions): void;
}

// @public (undocumented)
export interface BackendRegistrationPoints {
  // (undocumented)
  registerExtensionPoint<TExtensionPoint>(
    ref: ExtensionPoint<TExtensionPoint>,
    impl: TExtensionPoint,
  ): void;
  // (undocumented)
  registerInit<
    Deps extends {
      [name in string]: unknown;
    },
  >(options: {
    deps: {
      [name in keyof Deps]: ServiceRef<Deps[name]> | ExtensionPoint<Deps[name]>;
    };
    init(deps: Deps): Promise<void>;
  }): void;
}

// @public (undocumented)
export const cacheServiceRef: ServiceRef<PluginCacheManager>;

// @public (undocumented)
export const configServiceRef: ServiceRef<Config>;

// @public (undocumented)
export function createBackendModule<
  TOptions extends
    | {
        [name: string]: unknown;
      }
    | undefined = undefined,
>(
  config: BackendModuleConfig<TOptions>,
): undefined extends TOptions
  ? (options?: TOptions) => BackendFeature
  : (options: TOptions) => BackendFeature;

// @public (undocumented)
export function createBackendPlugin<
  TOptions extends
    | {
        [name: string]: unknown;
      }
    | undefined = undefined,
>(
  config: BackendPluginConfig<TOptions>,
): undefined extends TOptions
  ? (options?: TOptions) => BackendFeature
  : (options: TOptions) => BackendFeature;

// @public (undocumented)
export function createExtensionPoint<T>(options: {
  id: string;
}): ExtensionPoint<T>;

// @public (undocumented)
export function createServiceFactory<
  TService,
  TImpl extends TService,
  TDeps extends {
    [name in string]: unknown;
  },
>(factory: {
  service: ServiceRef<TService>;
  deps: TypesToServiceRef<TDeps>;
  factory(deps: DepsToDepFactories<TDeps>): Promise<FactoryFunc<TImpl>>;
}): ServiceFactory<TService>;

// @public (undocumented)
export function createServiceRef<T>(options: {
  id: string;
  defaultFactory?: (service: ServiceRef<T>) => Promise<ServiceFactory<T>>;
}): ServiceRef<T>;

// @public (undocumented)
export const databaseServiceRef: ServiceRef<PluginDatabaseManager>;

// @public (undocumented)
export type DepsToDepFactories<T> = {
  [key in keyof T]: (pluginId: string) => Promise<T[key]>;
};

// @public (undocumented)
export const discoveryServiceRef: ServiceRef<PluginEndpointDiscovery>;

// @public
export type ExtensionPoint<T> = {
  id: string;
  T: T;
  toString(): string;
  $$ref: 'extension-point';
};

// @public (undocumented)
export type FactoryFunc<Impl> = (pluginId: string) => Promise<Impl>;

// @public (undocumented)
export interface HttpRouterService {
  // (undocumented)
  use(handler: Handler): void;
}

// @public (undocumented)
export const httpRouterServiceRef: ServiceRef<HttpRouterService>;

// @public (undocumented)
export interface Logger {
  // (undocumented)
  child(fields: { [name: string]: string }): Logger;
  // (undocumented)
  info(message: string): void;
}

// @public (undocumented)
export const loggerServiceRef: ServiceRef<Logger>;

// @public (undocumented)
export function loggerToWinstonLogger(
  logger: Logger,
  opts?: TransportStreamOptions,
): Logger_2;

// @public (undocumented)
export const permissionsServiceRef: ServiceRef<
  PermissionAuthorizer | PermissionEvaluator
>;

// @public (undocumented)
export const schedulerServiceRef: ServiceRef<PluginTaskScheduler>;

// @public (undocumented)
export type ServiceFactory<TService = unknown> = {
  service: ServiceRef<TService>;
  deps: {
    [key in string]: ServiceRef<unknown>;
  };
  factory(deps: {
    [key in string]: unknown;
  }): Promise<FactoryFunc<TService>>;
};

// @public
export type ServiceRef<T> = {
  id: string;
  T: T;
  toString(): string;
  $$ref: 'service';
};

// @public (undocumented)
export const tokenManagerServiceRef: ServiceRef<TokenManager>;

// @public (undocumented)
export type TypesToServiceRef<T> = {
  [key in keyof T]: ServiceRef<T[key]>;
};

// @public (undocumented)
export const urlReaderServiceRef: ServiceRef<UrlReader>;
```
