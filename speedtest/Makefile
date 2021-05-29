.PHONY: run-without-docker-sync
run-without-docker-sync: ## docker-sync無し
	@docker-compose run --rm app


.PHONY: run-with-docker-sync
run-with-docker-sync: ## docker-sync有り
	@COMPOSE_FILE=docker-compose.yml:docker-compose.with-docker-sync.yml docker-compose run --rm app

.PHONY: start-sync
start-sync: ## docker-sync start -d
	@docker-sync start -d

.PHONY: clean-sync
clean-sync: ## docker-sync start -d
	@docker-sync clean

.PHONY: diff
diff: ## docker-sync有り・無しのdiff
	@echo '-----without docker-sync'
	@docker-compose config
	@echo '-----with docker-sync'
	@COMPOSE_FILE=docker-compose.yml:docker-compose.with-docker-sync.yml docker-compose config


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
