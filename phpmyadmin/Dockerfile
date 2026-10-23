FROM phpmyadmin:5.2.3-apache

LABEL maintainer="Bo-Yi Wu <appleboy.tw@gmail.com>"

# Refuse to build on a stale cached image still affected by PHP2Shell
# (CVE-2026-109618 / CVE-2026-109619): rebuild with `docker compose build --pull phpmyadmin`
RUN php -r '$fixed = ["8.2" => "8.2.35", "8.3" => "8.3.36", "8.4" => "8.4.27", "8.5" => "8.5.12"]; \
      $branch = PHP_MAJOR_VERSION . "." . PHP_MINOR_VERSION; \
      if (!isset($fixed[$branch]) || version_compare(PHP_VERSION, $fixed[$branch], "<")) { \
        fwrite(STDERR, "PHP " . PHP_VERSION . " is vulnerable to CVE-2026-109618 / CVE-2026-109619\n"); \
        exit(1); \
      }'

# Add volume for sessions to allow session persistence
VOLUME /sessions

# We expose phpMyAdmin on port 80
EXPOSE 80
