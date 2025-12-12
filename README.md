# webpack-config



### Add this in `Nextjs Config File.`

```
import type { NextConfig } from "next";


const nextConfig: NextConfig = {
  reactStrictMode: false,
  // Disable production source maps to reduce build size and disk usage
  // Enable only if you need them for debugging production issues
  productionBrowserSourceMaps: false,
  /* config options here */
  webpack(config, { dev, isServer }) {
    // Explicitly disable source maps in production to reduce build size and disk usage
    if (!dev) {
      config.devtool = false;
    } else if (!isServer) {
      // Use cheaper source maps in development to reduce cache size
      // 'eval-cheap-module-source-map' is faster and uses less disk space
      config.devtool = 'eval-cheap-module-source-map';
    }
    config.module.rules.push({
      test: /\.svg$/i,
      issuer: /\.[jt]sx?$/,
      use: [
        {
          loader: "@svgr/webpack",
          options: {
            icon: true,
          },
        },
      ],
    });

    return config;
  },
  turbopack: {
    rules: {
      '*.svg': {
        loaders: ['@svgr/webpack'],
        as: '*.js',
      },
    },
  },
  experimental: {
    serverActions: {
      bodySizeLimit: '50mb' // Increased from 2mb to 50mb
    },
    // Optimize memory usage during builds to prevent hangs
    webpackMemoryOptimizations: true,
  },
};

  ```
