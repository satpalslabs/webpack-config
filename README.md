# webpack-config



### Add this in `Nextjs Config File.`

```
const nextConfig: NextConfig = {
  reactStrictMode: false,
  productionBrowserSourceMaps: true, // enable source maps in prod
 webpack(config) {
    config.devtool = 'source-map'; // emit source maps in development
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
  experimental: {
    turbo: {
      rules: {
        '*.svg': {
          loaders: ['@svgr/webpack'],
          as: '*.js',
        },
      },
    },
    serverActions: {
      bodySizeLimit: '50mb' // Increased from 2mb to 50mb
    },
  }
}
  ```
