#-----------------singlestage------------------------
# # Use the official lightweight Node.js image
# FROM node:18-alpine

# # Set the working directory inside the container
# WORKDIR /app

# # Copy the application file into the container
# COPY server.js .

# # Expose the port the app runs on
# EXPOSE 3000

# # Command to run the application
# CMD ["node", "server.js"]


#-----------------multistage------------------------

    # ==============================================================================
# STAGE 1: Build and compile the application
# ==============================================================================
FROM node:18-alpine AS builder

WORKDIR /app

# Copy the source code
COPY server.js .

# Install the compilation tool and compile the script into a standalone binary
RUN npm install -g pkg && \
    pkg -t node18-linuxstatic-x64 server.js -o server

# ==============================================================================
# STAGE 2: Run the compiled artifact in a minimal base image
# ==============================================================================
FROM scratch

# Copy only the compiled binary artifact from the builder stage
COPY --from=builder /app/server /server

# Expose the application port
EXPOSE 3000

# Run the standalone binary
ENTRYPOINT ["/server"]
