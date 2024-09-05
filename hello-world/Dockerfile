# Use the official AWS Lambda Node.js 20.x base image
FROM public.ecr.aws/lambda/nodejs:20

# Set the working directory inside the container
WORKDIR /var/task

# Copy only the necessary files: package.json, package-lock.json
COPY package*.json ./

# Install production dependencies (and dev dependencies for build)
RUN npm install

# Copy the TypeScript source file (app.ts) and config file (tsconfig.json)
COPY app.ts ./
COPY tsconfig.json ./

# Install esbuild for bundling TypeScript
RUN npm install --save-dev esbuild

# Transpile TypeScript to JavaScript using esbuild
RUN npx esbuild app.ts --bundle --platform=node --target=node20 --outfile=dist/app.js

# Command to execute the transpiled code in AWS Lambda
CMD ["dist/app.lambdaHandler"]
