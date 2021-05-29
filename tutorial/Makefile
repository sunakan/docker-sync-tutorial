export COMPOSE_FILE=docker-compose.yml:docker-compose-dev.yml

.PHONY: config
config: ## compose config
	docker-compose config

.PHONY: up
up: ## compose up
	mkdir -p app
	touch app/somefile.txt
	docker-compose up

.PHONY: down
down: ## compose down
	docker-compose down

.PHONY: up-sync
up-sync: ## 同期開始
	mkdir -p app
	(docker volume inspect fullexample-sync > /dev/null 2>&1) || docker volume create fullexample-sync
	(docker volume inspect simpleexample-sync > /dev/null 2>&1) || docker volume create simpleexample-sync
	docker-sync start --foreground

.PHONY: down-sync
down-sync: ## 同期終了
	docker-sync clean

.PHONY: list
list: ## 同期中のvolume一覧
	docker-sync list

.PHONY: clean
clean: ## 片付け
	(docker volume inspect fullexample-sync > /dev/null 2>&1 && docker volume rm fullexample-sync) || echo ok
	(docker volume inspect simpleexample-sync > /dev/null 2>&1 && docker volume rm simpleexample-sync) || echo ok

.PHONY: test
test: ## make up 後 somefile.txt に追記
	echo 'hello' >> app/somefile.txt




################################################################################
# Utility-Command help
################################################################################
.DEFAULT_GOAL := help

################################################################################
# マクロ
################################################################################
# Makefileの中身を抽出してhelpとして1行で出す
# $(1): Makefile名
define help
  grep -E '^[a-zA-Z0-9_-]+:.*?## .*$$' $(1) \
  | grep --invert-match "## non-help" \
  | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'
endef
################################################################################
# タスク
################################################################################
.PHONY: help
help: ## Make タスク一覧
	@echo '######################################################################'
	@echo '# Makeタスク一覧'
	@echo '# $$ make XXX'
	@echo '# or'
	@echo '# $$ make XXX --dry-run'
	@echo '######################################################################'
	@echo $(MAKEFILE_LIST) \
	| tr ' ' '\n' \
	| xargs -I {included-makefile} $(call help,{included-makefile})
